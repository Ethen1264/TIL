# optimistic update

> Optimistic Update
>
> Optimistic Update는 네트워크 요청을 보내기 전에 UI를 업데이트하여, 사용자가 응답을 기다리지 않고 즉각적인 결과를 볼 수 있게 함으로써 사용자 경험을 개선하는 방법이다.

### 구현 방법

방법은 useMutation hook에서 onSuccess가 아니라 onMutate메서드와 onError메서드를 조합하여 구현할 수 있다.

```tsx
import React from "react";
import { useMutation, useQueryClient } from "@tanstack/react-query";

function useUpdateLike() {
  const queryClient = useQueryClient();

  return useMutation(
    (updatedPost) => {
      // API 호출 (예: PUT 요청)
      return fetch(`/api/posts/${updatedPost.id}/like`, {
        method: "PUT",
        body: JSON.stringify(updatedPost),
        headers: {
          "Content-Type": "application/json",
        },
      }).then((res) => res.json());
    },
    {
      // Optimistic Update 설정
      onMutate: async (updatedPost) => {
        await queryClient.cancelQueries(["posts", updatedPost.id]);

        const previousPost = queryClient.getQueryData([
          "posts",
          updatedPost.id,
        ]);

        queryClient.setQueryData(["posts", updatedPost.id], (old) => ({
          ...old,
          liked: updatedPost.liked,
          likesCount: updatedPost.liked
            ? old.likesCount + 1
            : old.likesCount - 1,
        }));

        return { previousPost };
      },
      // 에러 발생 시 롤백
      onError: (err, updatedPost, context) => {
        queryClient.setQueryData(
          ["posts", updatedPost.id],
          context.previousPost
        );
      },
      // 성공 시 업데이트된 데이터를 다시 불러오기
      onSettled: (updatedPost) => {
        queryClient.invalidateQueries(["posts", updatedPost.id]);
      },
    }
  );
}

function PostItem({ post }) {
  const updateLike = useUpdateLike();

  const handleLikeClick = () => {
    updateLike.mutate({ ...post, liked: !post.liked });
  };

  return (
    <div>
      <h2>{post.title}</h2>
      <p>{post.content}</p>
      <div>
        <button onClick={handleLikeClick}>
          {post.liked ? "💔" : "❤️"} {post.likesCount}
        </button>
      </div>
    </div>
  );
}

export default PostItem;
```

- queryClient.cancelQueries: posts와 해당 id에 대한 기존 쿼리를 일시적으로 중단하여 불필요한 중복 요청을 방지한다.
- queryClient.getQueryData: 캐시에서 현재 posts 데이터 중 해당 id를 가진 항목을 가져온다.
- queryClient.setQueryData: 캐시 데이터를 업데이트한다.
  ```tsx
  queryClient.setQueryData(["posts", updatedPost.id], (old) => ({
    ...old,
    liked: updatedPost.liked,
    likesCount: updatedPost.liked ? old.likesCount + 1 : old.likesCount - 1,
  }));
  ```
  - 이떄 old는 기존의 post 데이터이다.
- onError: 요청이 실패했을 때 호출된다. context.previousPost를 사용해 캐시 데이터를 원래 상태로 롤백한다.
- onSettled: 변이가 성공하든 실패하든 상관없이 호출된다. 캐시된 데이터를 최신 상태로 유지하기 위해 invalidateQueries를 사용해 쿼리를 무효화하고 다시 데이터를 가져온다.
