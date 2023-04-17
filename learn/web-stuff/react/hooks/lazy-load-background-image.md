---
description: Example usage of react custom hook to lazy load background image.
---

# Lazy load background image

One of the common senario when optimising image focused website is to lazy load the image. \
\
There is already many example of how to lazy load an image. However, we don't see much of the background image being used for lazy load.\
\
One of the way we can lazy load image in react is by using react custom hook & web api IntersectionObserver.

```typescript
import { MutableRefObject, useEffect, useRef, useState } from "react";

export function useLazyBackgroundImage(
  elem: MutableRefObject<HTMLElement | null>,
  src: string
) {
  const [el, setEl] = useState(elem);
  const observable = useRef<IntersectionObserver | null>(null);
  const [imgSrc, setImgSrc] = useState("https://picsum.photos/200"); //Set a default fallback image.
  const opt = {}; // Default options but can be changed as needed.
  const loadImage = () => {
     const img = new Image();
     img.src = src;
     img.onload = (): void => setImgSrc(src);
  }
  const cb = (
    entries: IntersectionObserverEntry[],
    observer: IntersectionObserver
  ): void => {
    entries.forEach((entry) => {
      if (
        el.current &&
        observable.current &&
        (entry.isIntersecting || entry.intersectionRatio > 0)
      ) {
        observable.current.unobserve(el.current);
        loadImage(); // We can change the callback to something else.
      }
    });
  };

  useEffect(() => {
    if (window) {
      observable.current = new IntersectionObserver(cb, opt);
      if (el.current && observable.current)
        observable.current.observe(el.current);
    }
    return () => {
      if (observable) {
        if (el.current && observable.current)
          observable.current.unobserve(el.current);
      }
    };
  }, [elem]);

  return imgSrc;
}

// Usage
function SomeBackgroundComponent() {
  const image_url= 'https://picsum.photos/200';
  const elem = useRef(null);
  const imageSource = useLazyBackgroundImage(
    elem,
    image_url
  );
  
  return (
    <div
      ref={elem}
      style={{
        backgroundImage: `url(${imageSource})`,
      }} />
  );
}
```

Here we are simply using IntersectionObserver to watch for a specific DOM element to come into view port than run a callback that loads the image and finally stop listening/watching that element as we already have image downloaded.

In above code we can see how we can easily change the code base to make it more generic so it can be used for more than just background image and be more re-useable. Like adding few new param to set configuration for IntersectionObserver or adding a custom callback to run some other task instead of loading image.

