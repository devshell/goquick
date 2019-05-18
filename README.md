# goquick
Golang Scaffolding

Take a db model struct in go and translate it into a JSON form, and then (using reactjs) generate the form and handle communications between server and client for said form.

REST end-point should be ala ".../form/id/23287".

1. if it gets a request with an initial value indicating that this is the first time the form is being generated, it responds with the form definition from the server for your client to generate the form in react, with the initial value now set to false.
2. if the server gets a request with an initial value set to false, the client form submission is checked through the form validation and the result is returned the form definition back to the client with errors raised by server-side validation.
3. if the server gets a request that is valid, the server will respond with the form definition and the other header values set, such as next and message.

So the JSON would initially look like this. I was working on something like this for go called "goscaffolding":
```
{
    form: {
        get: ".../form/id/23287"
        init: "false",
        next: "",
        message: "",
        csrf: "sdaf9889df9889dsf88df89dsflkjsdf898",
        form-element: {  // generated from the db model and types for db fields (i.e. boolean db type = radio)
            input: {
                type: "number",
                id: "1",
                name: "age",
                value: "18",
                hint: "Your age must be between 18 and 180 years old.",
                error: "",   //filled by the server if validated to be invalid
            }
        }
    }
}
```
