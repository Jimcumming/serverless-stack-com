---
layout: post
title: List All the Notes
date: 2017-01-26 00:00:00
lang: en
ref: list-all-the-notes
description: We want to display all the notes a user has in our React.js app. To do this we are going to use our Home container and render a list if a user is logged in.
context: true
comments_id: list-all-the-notes/156
---

Now that we are able to create a new note, let's create a page where we can see a list of all the notes a user has created. It makes sense that this would be the homepage (even though we use the `/` route for the landing page). So we just need to conditionally render the landing page or the homepage depending on the user session.

Currently, our Home container is very simple. Let's add the conditional rendering in there.

<img class="code-marker" src="/assets/s.png" />Replace our `src/containers/Home.js` with the following.

``` coffee
import React, { useState, useEffect } from "react";
import { PageHeader, ListGroup } from "react-bootstrap";
import "./Home.css";

export default function Home(props) {
  const [notes, setNotes] = useState([]);
  const [isLoading, setIsLoading] = useState(true);

  function renderNotesList(notes) {
    return null;
  }

  function renderLander() {
    return (
      <div className="lander">
        <h1>Scratch</h1>
        <p>A simple note taking app</p>
      </div>
    );
  }

  function renderNotes() {
    return (
      <div className="notes">
        <PageHeader>Your Notes</PageHeader>
        <ListGroup>
          {!isLoading && renderNotesList(notes)}
        </ListGroup>
      </div>
    );
  }

  return (
    <div className="Home">
      {props.isAuthenticated ? renderNotes() : renderLander()}
    </div>
  );
}
```

We are doing a few things of note here:

1. Rendering the lander or the list of notes based on `props.isAuthenticated`.

2. Store our notes in the state. Currently, it's empty but we'll be calling our API for it.

3. Once we fetch our list we'll use the `renderNotesList` method to render the items in the list.

And that's our basic setup! Head over to the browser and the homepage of our app should render out an empty list.

![Empty homepage loaded screenshot](/assets/empty-homepage-loaded.png)

Next we are going to fill it up with our API.
