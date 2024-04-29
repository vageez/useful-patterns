# useful-patterns

# HOC data fetching layer

```
const WithQuery = (Component, Skeleton) => {
  // @param id - unique id to fetch content, passed in at the time of calling the HOC
  const WithContents = (id) => {
    const [content, setContent] = useState();
    const fetch = (id) =>
      Promise.resolve().then((data) => {
        setContent(data);
      });
    useEffect(() => {
      const timer = setTimeout(() => fetch(id), 1000);

      return () => {
        clearTimeout(timer);
      };
    }, []);

    if (content) {
      return <Component {...content} />;
    } else {
      return <Skeleton />;
    }
  };

  WithContents.displayName = "WithContents";
  return WithContents;
};

import React, { useEffect, useState } from "react";

export default WithQuery;


```
