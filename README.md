## 🚀 Quick start
## Getting started
1. Create .env file and add values provided from us
2. yarn install
3. After installation: yarn dev
4. After site builds, navigate to site(either localhost:8000 or localhost:8001)
5. Make edits to hero subtitle content on Tipe (many steps)
6. Make hero title dynamic and add to Tipe (many steps)
    1. Extra: Make subtitle handle and support markdown
    2. Extra: Add nav links top Tipe

## What is Tipe
* editor that lives in your application
* real time edits
* custom components

### gatsby-theme-tipe
```javascript
// gatsby-config.js

{
  plugins: [
    resolve: `@tipe/gatsby-theme-tipe`, -- this is our theme
      options: {
        // this is the relative path on your existing site that you will find your tipe theme dashboard
        // ex: localhost:yoursiteroot/tipe
        basePath: '/tipe',
        // this is your tipe project id
        project: process.env.TIPE_PROJECT,
        // this is your tipe projects environment
        environmentForSdk: process.env.TIPE_ENVIRONMENT,
        // path to your schema
        schemaPath: path.resolve('./src/tipe'),
        // your tipe apikey
        apiKey: process.env.TIPE_API_KEY,
      },
  ]
}
```

# Create a schema
## Schema
* A schema is: A javascript object that contains templates keyed by their names

## Templates
* A template is: A javascript object that defines the shape of a document

## Fields
* A field is: A javascript object that defines the type of a value

* Here is an example or a plain home page template with a single H1 tag
``` javascript
  HomePage: {
    // this is the default template type
    template: document,
    // Scott
    type: HomePage,
    // this is what will be displayed in the editor ui
    name: Home Page,
    // where you define your content
    fields: {
      // this is the identifier that will be used in lookup
      title: {
        // its a primative string type that will render a default text input
        type: string,
        // this is what will be displayed in the editor ui
        name: title
      }
    }
  }
```
## Types

### Primitives (String, Number, Boolean)

### Collections (Object, Array) - ultimately boil down to primatives

#### Array
* **array** renders a list of elements, **contains** restricts values allowed in the list and is required
  ``` javascript
    exampleArray: {
      type: array,
      contains: [{ type: string }, { type: number }, { type: boolean }]
    }
  ```

#### Object
* **object** has fields that can be a primative or another type 
``` javascript
  exampleObject: {
    template: object,
    fields: {
      exampleString: {
        type: string,
        name: example
      }
    }
  }

  exampleObject2: {
    template: object,
    fields: {
      exampleString2: {
        type: exampleObject,
        name: example2
      }
    }
  }
```
#### Custom components
* Tipe supports custom components that allow you to customize your editor in anyway you wish. There are 2 simple props that we require a change handler (onChange) and a value prop
``` javascript
const customComponent = props => {
  return (
    <input value={props.value} onChange={props.setValue}/>
  )
}
```
