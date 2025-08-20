### Next.js ###

# ##🧑‍🏫 Step 1: What is Next.js?##

  . React is just a library. It only cares about components.
  . Next.js is a framework built on React that solves the stuff you need to actually ship a full app:
   . 📍 Routing:- Pages and navigation without react-router.
   . ⚡ Server-Side Rendering (SSR):- Generates HTML on the server for SEO and speed.
   . 📦 Static Site Generation (SSG):- Build pages at build time (super fast hosting)
   . 🌍 API Routes:- You can make backend endpoints inside your project.
   . 📑 File-based routing:- just make files in pages/ and they become routes.

So you can think: Next.js = React + Node server + routing + SSR/SSG + API

### 🛠 Step 2: Install Next.js ###

Run:

   npx create-next-app@latest my-next-app
   cd my-next-app
   npm run dev


Visit 👉 http://localhost:3000
 → you’ll see a starter page.


### 📂 Step 3: Folder structure ###

my-next-app/
   pages/      <-- Each file here is a route
     index.js    <-- route: "/"
     about.js    <-- route: "/about"
     api/
       hello.js  <-- route: "/api/hello"
   public/       <-- static assets (image, etc.)
   styles/       <-- css modules
   next.config.js <-- Next.js config

. If you add pages/about.js -> visiting /about works automatically.

Example:- 

     // pages/about.js
    export default function About(){
        return <h1>About Us</h1>
    }

### 🧑‍💻 Step 4: Pages & routing ###

. pages/index.js -> /
. pages/about.js -> /about
.Dynamic routes:
    . pages/user/[id].js -. /user/123 or /user/abc

Example:-
  
  // pages/user/[id].js

  import { useRouter } from "next/router";

  export default function UserPage(){
     const router = useRouter();
     return <h1>User ID: {router.query.id}</h1>;
  }
  

### 🌐 Step 5: API routes (backend inside Next.js) ###

In pages/api/hello.js:

    export default function handler(req, res){
         res.status(200).json({ message: "Hello from API!" });
    }

   . Now visit http://localhost:3000/api/hello
  . → you get JSON.
    This is like having a mini backend (good for chat, login, etc.).

### step 6 :- Server-Side Rendering(SSR) ###

  Use getServerSideProps if you want data fetched at request time.

  //pages/ssr.js

  export async function getServerSideProps(){
      const res = await fetch("https://jsonplaceholder.typicode.com/posts/1");
      const post = await res.json();
      return { props: {post} };
  }

  export default function SSRPage({ post }){
      return <div><h1>{post.title}</h1><p>{post.body}</p></div>;
  }

  Visiting /ssr → the HTML is generated on the server before sending to browser (great for SEO).


### 📦 Step 7: Static Site Generation (SSG) ###
Use getStaticProps if the data doesn’t change often (blog, docs).

// pages/static.js

// pages/static.js
export async function getStaticProps() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts/2");
  const post = await res.json();
  return { props: { post } };
}

export default function StaticPage({ post }) {
  return <div><h1>{post.title}</h1><p>{post.body}</p></div>;
}


The page is built once at build time → super fast.


### step 8: Deployment ###
Next.js apps are production-ready and easiest to deploy on Vercel (the company that made Next.js).

just run:

    npm run build 
    npm run start

or push to GitHub and connect to Vercel.
   
     