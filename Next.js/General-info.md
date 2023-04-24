##Folders
###Pages folder
This is where your pages are located. Next.js has a file based router, meaning that your URL-links are based on the location and filename of your page. for example a file located in folder api/test will have URL: www.samplepage.com/api/test

###Public folder
This is where you can serve public assets from, such as favicons, or other images.

###Styles folder
Here your styles are located.


##How to start your application
Go to the package.json file, in which you will find different scripts, such as dev, build, start or lint.

You can start your application by executing command `yarn <scriptname>`, for example: `yarn dev`.

If you want to run a server you need to build the application using `yarn build`, and you can then run it using `npx serve out`.


##Specific files
**pages/_app.tsx** is going to wrap every single page. Meaning that every single thing you add in the return function of that file, will be visible on every page.


##Getting started
###Static page
You want to start by adding a `export const getStaticProps` function to your index.txs file. The syntax is as follows: 
`export const getStaticProps = async (context) => { function logic here }`
The alternative to this is getServersideProps:
`export const getServerSideProps = async (context) => { function logic here }`

What these functions do is they retrieve the data that is required for this page to load, for example it can retrieve all of the data from an API endpoint.

Because we are using TypeScript, we're going to use types.
We're going to modify our methods:
`export const getStaticProps: GetStaticProps = async (context) => { method logic here }`
Or
`export const getServerSideProps: GetServerSideProps = async (context) => { method logic here }`

Code example of what one of these functions could look like:
```
export const getStaticProps: GetStaticProps = async (context) => {
  const res = await fetch("https://rickandmortyapi.com/api/character");
  const {results}:GetCharacterResults = await res.json();

  return {
    props: {
      characters: results,
    },
  };
};
```
###Dynamic page
You can dynamically create pages, this can be usefull in situations where you have many objects that are similar but each need their own page, like for example with a website that sells shoes. Each shoe must have their own page, but you can't create a new page for every single shoe cause there would be hundreds of pages eventually.

To create a dynamic page you can name the file `[id].tsx` (put it inside the pages folder).


