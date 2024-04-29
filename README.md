# useful-patterns

# HOC data fetching layer

```
// file comp/with-io.js

const WithIO = (Component, Skeleton) => {
  // @param id - unique id to fetch content, passed in at the time of calling the HOC
  const FetchContents = (id) => {
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

  FetchContents.displayName = "FetchContents";
  return FetchContents;
};

import React, { useEffect, useState } from "react";

export default WithIO;

// USAGE
// file comp/index.js

import WithIO from 'with-io'

export default WithIO(ReactComponent, ReactSkeletonComponent);

// USAGE

import Component from 'comp/index'

<Component id={123abc}/>

```
