# HTTP Sessions

## What is a Session?

A session is a way for a server to remember who you are between requests.

Without a session, every HTTP request would appear to come from a brand new user.

---

## Cookie vs Session ID

A cookie is a small piece of data stored in the browser.

A session ID (or session token) is the value often stored inside that cookie.

Example:

Cookie

sessionid = a8f3c91d4b7e12f...

In this example:

- Cookie = the container
- Session ID = the unique value inside it

---

## Mental Model

Think of it like this:

Cookie = Envelope

Session ID = Letter inside the envelope

The browser stores the envelope.

The server reads the letter.

---

## How a Login Works

1. User logs in.
2. Server creates a unique session ID.
3. Server stores session information.
4. Server sends the session ID back inside a cookie.
5. Browser stores the cookie.
6. Browser sends the cookie with every future request.
7. Server recognizes the session ID and knows who the user is.

---

## Important Note

A cookie can store many kinds of information.

It is **not** always a session ID.

Sometimes it stores:

- Preferences
- Language
- Theme
- Analytics IDs

A session ID is simply one common use for a cookie.

---

## Engineering Takeaway

The cookie is the container.

The session ID is the identity.
