```js
const throttle = (fn, throttleTime) => {
  let isLocked = false;
  const lock = () => (isLocked = true);
  const unlock = () => (isLocked = false);

  return function (...args) {
    if (isLocked) return;

    fn.apply(this, args);
    lock();

    setTimeout(() => {
      unlock();
    }, throttleTime);
  };
};
```