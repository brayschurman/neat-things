# Async

## Synchronous versus Asynchronous

In a **synchronous** system, tasks are completed one after the other.

In an **asynchronous** system, tasks are completed independent of one another.

- beneficial in situations where we would like the program to proceed and not _wait_ for the return (API call, fetch, image processing). This even works on single-threaded stuff like JavaScript.

## Async Await

- async functions always return a promise

- only when a function is declared as **async**, you can prepend calls inside of it with **await**

```javascript
async function f() {

    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve("done), 1000)
    });

    let result = await promise;

    return result;
}

```

The JavaScript engine will pause execution at the **await** line and proceed with other tasks until it gets a result. Another example:

```javascript

async function showAvatar() {

  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();

  let githubResponse = await fetch(`https://api.github.com/users/${user.name}`);
  let githubUser = await githubResponse.json();

  let img = document.createElement('img');
  img.src = githubUser.avatar_url;
  img.className = "promise-avatar-example";
  document.body.append(img);

  await new Promise((resolve, reject) => setTimeout(resolve, 3000));

  img.remove();

  return githubUser;
}

showAvatar();

```