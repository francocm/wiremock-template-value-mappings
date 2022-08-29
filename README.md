# wiremock-template-value-mappings

## Summary

Attempting to use Wiremock standalone with global response templating to dynamically map an input value (`user id`) with a response value (`username`).

This repo is set up to demonstrate the issue I'm coming up against: _unable to fetch a value from `transformerParameters.*` dynamically_.

This repo serves mainly the purpose of referencing it in a [Stack Overflow question](https://stackoverflow.com/questions/73531968/wiremock-dynamic-mapping-of-response-values).

My goal is to populate the `username` field in the JSON response based dynamically on the input user ID, by using the JSON map under `transformerParameters.usernameMapping`.

I have tried:

* `{{parameters.usernameMapping.2}}` <-- works but hardcoded so does not solve our problem
* `{{parameters.usernameMapping[request.pathSegments.[1]]}}` <-- breaks
* `{{parameters.usernameMapping[{{request.pathSegments.[1]}}]}}` <-- breaks
* `{{parameters.usernameMapping.{{request.pathSegments.[1]}}}}` <-- breaks

You can view the mapping [here](stubs/mappings/example-get-user.json).

You can call the stub via `curl` using:

```bash
curl --location --request GET 'http://localhost:8080/users/1' \
    --header 'Accept: application/json'
```

To run this, assuming you have [Docker (Compose)](https://www.docker.com/): `docker compose up -d` _(it will bind to port `8080`)_.

I am trying to resolve this without having to write custom extensions to Wiremock, and I am wondering what I might be missing here.

***EOF***   
