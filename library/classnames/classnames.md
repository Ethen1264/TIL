# classnames

classnames 모듈은 여러 클래스를 추가할 때 뿐만 아니라, 특정 값이 true/false임에 따라 클래스명을 추가하거나, 추가하지 않도록 하는 것을 간단히 구현할 수 있게 해준다.

```
yarn add classnames
```

### 예시코드

```tsx
import style from './post.module.css';
import cx from 'classnames';

export default function ActionButtons() {
  const commented = true;
  const reposted = true;
  const liked = false;

  return <div className={cx(style.commentButton, { [style.commented]: commented })}>{/* ... */}</div>;
}
```

위의 코드의 `[style.commented]: commented`의 commented가 true라면 classname이 commentButton, commented인 스타일이 적용되며 false라면 commentButton인 스타일이 적용된다.

```tsx
import classNames from ‘classnames’;


classNames(‘one’, ‘two’); // = ‘one two‘
classNames(‘one’, { two: true }); // = ‘one two‘
classNames(‘one’, { two: false }); // = ‘one‘
classNames(‘one’, [‘two’, ‘three’]); // = ‘one two three‘



const myClass = ‘hello’;
classNames(‘one’, myClass, { myCondition: true }); // = ‘one hello myCondition'
```
