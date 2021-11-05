```typescript
import { useState, useEffect } from 'react';

function getCurrentDeviceWidth() {
  const { innerWidth: width, innerHeight: height } = window;
  return {
    width,
    height,
  };
}

export default function useCurrentDeviceWidth(): { width: number; height: number } {
  const [windowDimensions, setCurrentDeviceWidth] = useState(getCurrentDeviceWidth());

  useEffect(() => {
    function handleResize() {
      setCurrentDeviceWidth(getCurrentDeviceWidth());
    }

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return windowDimensions;
}
```