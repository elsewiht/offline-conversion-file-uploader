# Get Prepared

Fill the placeholder in the following script and then execute. The script installs and compiles the tool, and set the necessary parameter(ad account / audience ID and access token) for demo.

```
npm install
npm run compile
cd demo-audience; unzip test-audience-files.zip; cd ..
export audience_id='YOUR_CUSTOM_AUDIENCE_ID_HERE'
export access_token='YOUR_ACCESS_TOKEN_HERE'
```

If you don't have audience ID yet, you can use ad account ID.
```
export ad_account_id='YOUR_AD_ACCOUNT_ID_HERE'
```
Then when adding users, replace `--customAudienceID $audience_id` with `--adAccountID $ad_account_id`. The tool will auto create an ID for you. When deleting users from custom audiece, audience ID is always required.

# Run Demos

## Data File Custom Audience

### Only Email

Add users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-email-10k.json \
  --inputFilePath demo-audience/test-email-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id
```

Delete users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-email-10k.json \
  --inputFilePath demo-audience/test-email-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id \
  --removeUsers
```

### Various PII Data (Clean)

Add users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-rich-10k.json \
  --inputFilePath demo-audience/test-rich-clean-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id
```

Delete users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-rich-10k.json \
  --inputFilePath demo-audience/test-rich-clean-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id \
  --removeUsers
```

### Various PII Data (Dirty file with errors)

Add users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-rich-10k.json \
  --inputFilePath demo-audience/test-rich-dirty-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id
```

The above command will fail because it will abort upload after detecting that more than 10% of the sample rows contain error. Use `--ignoreSampleErrors` option to forcefully upload.

## Value-based Lookalike Audience

If you are using `customAudienceID`, please make sure the corresponding custom audience is value-based.

### Only Email and Value

Add users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-email-value-10k.json \
  --inputFilePath demo-audience/test-email-value-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id
```

Remove users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-email-value-10k.json \
  --inputFilePath demo-audience/test-email-value-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id \
  --removeUsers
```

Value is not required to remove users from value-based custom audience, so you can also remove like how you remove from ordinary data-file custom audience:

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-email-10k.json \
  --inputFilePath demo-audience/test-email-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id \
  --removeUsers
```

### Various PII Data and Value (Clean)

Add users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-rich-value-10k.json \
  --inputFilePath demo-audience/test-rich-clean-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id
```

Remove users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-rich-value-10k.json \
  --inputFilePath demo-audience/test-rich-clean-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id \
  --removeUsers
```


### Various PII Data and Value (Dirty)

Add users

```
node lib/cli.js upload-audience \
  --configFilePath demo-audience/config-test-rich-value-10k.json \
  --inputFilePath demo-audience/test-rich-dirty-10k.csv \
  --accessToken $access_token \
  --customAudienceID $audience_id
```

The above command will fail because it will abort upload after detecting that more than 10% of the sample rows contain error. Use `--ignoreSampleErrors` option to forcefully upload.

