### Here's how I was able to start my dishwasher using [Home Connect REST API](https://api-docs.home-connect.com/quickstart/#the-home-connect-api)

This is a companion to [Home Connect's Quickstart](https://api-docs.home-connect.com/quickstart), documenting some gotchas I ran into.

- *Step 1: Get the Client ID*: As part of registering the application, you will be asked type of `OAuth Flow`. Select `Authorization Code Grant Flow`.
- *Step 2: Authorization URL and Response*
  - Request looks something like `https://api.home-connect.com/security/oauth/authorize?response_type=code&client_id=MY_CLIENT_ID&scope=IdentifyAppliance Dishwasher&redirect_uri=https://example.com`. Scope `IdentifyAppliance Dishwasher` is sufficient for running dishwasher.
  - After the oauth flow, you will be redirected to something like `https://example.com/?code=ey333330%3D&grant_type=authorization_code`. For next step, `code` starts at `ey` and ends at `0`; it doesn't not include the `%3D` at the end.
- *Step 3: Retrieve Token*: To get client secret, edit on Edit button for your dishwasher Application.
- Now I have access token. Quickstart implies I can use swagger. If you click on this link, a swagger page opens up:

  ![Screen Shot 2024-01-15 at 12 16 32 PM](https://github.com/melissachang/bosch-dishwasher-delayed-start/assets/10929390/d28e02c6-7fe1-4aae-a895-60ecb8497fab)

  However, I couldn't get Authorization to work. I think if Home Connect modified its Swagger specification to use Bearer token Authorization, then it would work. I also couldn't get postman to work.

  So the rest of the steps are with curl. You *can* use Swagger page to see endpoints and generate sample curl commands.

- Call [appliances/get_home_appliances](https://apiclient.home-connect.com/?client_id=1DDE83C96EB378181FEC379FD685BBD9F52311FEE0EA299AC06E96234566E9E2#/appliances/get_home_appliances) to get your dishwasher `haId`.
  ```
  curl -X GET "https://api.home-connect.com/api/homeappliances" -H "Authorization: Bearer MY_ACCESS_TOKEN"
  ```  
- Call [programs/start_program](https://apiclient.home-connect.com/?client_id=1DDE83C96EB378181FEC379FD685BBD9F52311FEE0EA299AC06E96234566E9E2#/programs/start_program) to start your dishwasher. It should start within seconds; you'll hear it running.
  ```
  curl -X 'PUT' 'https://api.home-connect.com/api/homeappliances/MY_HAID/programs/active'  -H 'Authorizatio: Bearer MY_ACCESS_TOKEN' -H 'accept: application/vnd.bsh.sdk.v1+json' -H 'Content-Type: application/vnd.bsh.sdk.v1+json' -d '{"data": {"key": "Dishcare.Dishwasher.Program.Auto2"}}'
  ```  
