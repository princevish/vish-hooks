# Notice: Package Deprecation

> We would like to inform you that the 'vish-hooks' package is now deprecated. We recommend trying our new '@princevish/vish-hooks2' package, which offers an enhanced experience with more features.

> Thank you for your understanding and continued support.

## Vish-hooks React Hooks

This project includes a set of custom React hooks. Here are the hooks and their usage examples:

## Table of Contents

- [Notice: Package Deprecation](#notice-package-deprecation)
  - [Vish-hooks React Hooks](#vish-hooks-react-hooks)
  - [Table of Contents](#table-of-contents)
  - [usePagination](#usepagination)
  - [useDeviceDetection](#usedevicedetection)
  - [useQueryParam](#usequeryparam)
  - [useFocusRef](#usefocusref)
  - [useIsFirstRender](#useisfirstrender)
  - [useIsMounted](#useismounted)
  - [usePrevious](#useprevious)
  - [useSWR](#useswr)
  - [useToggle](#usetoggle)
  - [useTimeout](#usetimeout)
  - [useUpdateEffect](#useupdateeffect)
  - [useEffectOnce](#useeffectonce)
  - [useClickOutside](#useclickoutside)
  - [useArray](#usearray)
  - [useDebounce](#usedebounce)
  - [useHover](#usehover)
  - [useFocus](#usefocus)

## usePagination

This hook allows you to manage pagination.

```javascript
import React, { useState } from "react";
import { usePagination } from "vish-hooks";

const MyComponent = () => {
  const [currentPage, setCurrentPage] = useState(1);
  const pageSize = 10;
  const totalCount = 100;

  const [paginationRange, DOTS] = usePagination({
    totalCount,
    pageSize,
    currentPage,
  });

  const handlePageChange = (pageNumber) => {
    setCurrentPage(pageNumber);
  };

  return (
    <div>
      <ul>
        {paginationRange.map((pageNumber, index) => (
          <li key={index}>
            {pageNumber === DOTS ? (
              <span>...</span>
            ) : (
              <button
                onClick={() => handlePageChange(pageNumber)}
                disabled={currentPage === pageNumber}
              >
                {pageNumber}
              </button>
            )}
          </li>
        ))}
      </ul>
      {/* Render your content based on the current page and page size */}
      <div>{/* Content for the current page */}</div>
    </div>
  );
};
```

## useDeviceDetection

This hook allows you to detect the device type.

```javascript
import React from "react";
import { useDeviceDetection } from "vish-hooks";

const MyComponent = () => {
  const { isMobile, isDesktop } = useDeviceDetection();

  return (
    <div>
      {isMobile && <p>You are on a mobile device.</p>}
      {isDesktop && <p>You are on a desktop device.</p>}
    </div>
  );
};
```

## useQueryParam

This hook allows you to manage query params.

```javascript
import React from "react";
import { useQueryParam } from "vish-hooks";

const MyComponent = () => {
  const [searchQuery, setSearchQuery] = useQueryParam("q", "");

  const handleSearchChange = (event) => {
    setSearchQuery(event.target.value);
  };

  return (
    <div>
      <input
        type="text"
        value={searchQuery}
        onChange={handleSearchChange}
        placeholder="Search..."
      />
      <p>Current search query: {searchQuery}</p>
    </div>
  );
};

```

## useFocusRef

This hook allows you to manage focus on a particular element.

```javascript
import { useFocusRef } from "vish-hooks";

const Component = () => {
  const [ref, isFocused] = useFocusRef();

  return <input ref={ref} />;
};
```

## useIsFirstRender

This hook allows you to check if the component is rendered for the first time.

```javascript
import { useIsFirstRender } from "vish-hooks";

const Component = () => {
  const isFirstRender = useIsFirstRender();

  return <div>{isFirstRender ? "First Render" : "Not First Render"}</div>;
};
```

## useIsMounted

This hook allows you to check if the component is mounted.

```javascript
import { useIsMounted } from "vish-hooks";

const Component = () => {
  const isMounted = useIsMounted();

  return <div>{isMounted ? "Mounted" : "Not Mounted"}</div>;
};
```

## usePrevious

This hook allows you to get the previous value of a state.

```javascript
import { usePrevious } from "vish-hooks";

const Component = () => {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);

  return (
    <div>
      <p>
        Current: {count} - Previous: {prevCount}
      </p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

## useSWR

This hook allows you to fetch data using SWR.

```javascript
import { useSWR } from "vish-hooks";

const Component = () => {
  const { data, error } = useSWR(
    "https://jsonplaceholder.typicode.com/todos/1"
  );

  if (error) return <div>failed to load</div>;
  if (!data) return <div>loading...</div>;

  return <div>{data.title}</div>;
};
```

## useToggle

This hook allows you to toggle between two states.

```javascript
import { useToggle } from "vish-hooks";

const Component = () => {
  const [isOn, toggleIsOn] = useToggle(false);

  return (
    <div>
      <p>{isOn ? "ON" : "OFF"}</p>
      <button onClick={toggleIsOn}>Toggle</button>
    </div>
  );
};
```

## useTimeout

This hook allows you to set a timeout.

```javascript
import { useTimeout } from "vish-hooks";

const Component = () => {
  const [isReady, cancel, reset] = useTimeout(5000);

  return (
    <div>
      <p>{isReady ? "Ready" : "Not Ready"}</p>
      <button onClick={cancel}>Cancel</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
};
```

## useUpdateEffect

This hook allows you to run an effect only when the component is updated.

```javascript
import { useUpdateEffect } from "vish-hooks";

const Component = () => {
  const [count, setCount] = useState(10);

  useUpdateEffect(() => {
    console.log("Updated");
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

## useEffectOnce

This hook allows you to run an effect only once.

```javascript
import { useEffectOnce } from "vish-hooks";

const Component = () => {
  useEffectOnce(() => {
    console.log("Mounted");
  });

  return <div>Mounted</div>;
};
```

## useClickOutside

This hook allows you to detect clicks outside a particular element.

```javascript
import { useClickOutside } from "vish-hooks";

const Component = () => {
  const ref = useRef();
  const [isModalOpen, setModalOpen] = useState(false);

  useClickOutside(ref, () => setModalOpen(false));

  return (
    <div>
      {isModalOpen ? (
        <div ref={ref}>
          <p>Click outside this element to close</p>
        </div>
      ) : (
        <button onClick={() => setModalOpen(true)}>Open Modal</button>
      )}
    </div>
  );
};
```

## useArray

This hook allows you to manage an array.

```javascript
import { useArray } from "vish-hooks";

const Component = () => {
  const [todos, { push, remove, filter, update }] = useArray([
    { id: 1, text: "Learn React" },
    { id: 2, text: "Learn Firebase" },
    { id: 3, text: "Learn GraphQL" },
  ]);

  return (
    <div>
      <button onClick={() => push({ id: 4, text: "Learn Hooks" })}>
        Add Todo
      </button>
      <button onClick={() => update(1, { id: 1, text: "Learn Hooks" })}>
        Update Todo
      </button>
      <button onClick={() => remove(1)}>Remove Todo</button>
      <button onClick={() => filter((todo) => todo.id !== 1)}>
        Remove Todo
      </button>
      {todos.map((todo) => (
        <div key={todo.id}>{todo.text}</div>
      ))}
    </div>
  );
};
```

## useDebounce

This hook allows you to debounce a value.

```javascript
import { useDebounce } from "vish-hooks";

const Component = () => {
  const [value, setValue] = useState("");
  const debouncedValue = useDebounce(value, 500);

  return (
    <div>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
        placeholder="Search..."
      />
      <p>Actual value: {value}</p>
      <p>Debounced value: {debouncedValue}</p>
    </div>
  );
};
```

## useHover

This hook allows you to detect if the mouse is over a particular element.

```javascript
import { useHover } from "vish-hooks";

const Component = () => {
  const [hoverRef, isHovered] = useHover();

  return (
    <div ref={hoverRef}>
      {isHovered ? <p>Move the mouse out of here!</p> : <p>Hover over me!</p>}
    </div>
  );
};
```

## useFocus

`useFocus` is a custom React hook that allows you to track whether the user's browser is currently focused on your application or not.

```javascript
import React from "react";
import { useFocus } from "vish-hooks";

const Component = () => {
  const [isFocused, setIsFocused] = useFocus();

  return (
    <div>
      {isFocused ? "The window is focused" : "The window is not focused"}
    </div>
  );
};
```
