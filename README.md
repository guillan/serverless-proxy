# Serverless Proxy

This repo is linked to the following article: [https://glannebere.medium.com/serverless-proxy-with-aws-api-gateway-and-aws-lambda-c09bd1c20c84](https://glannebere.medium.com/serverless-proxy-with-aws-api-gateway-and-aws-lambda-c09bd1c20c84)


**Prerequisite**

Serverless Framework needs to be installed: check documentation [here](https://www.serverless.com/framework/docs/providers/aws/guide/installation/)

---

To start, update the following variable in the serverless.yml:
- url
- vpcId
- subnetIds

Once it's done, if you don't need the resource policy part, remove this part in serverless.yml:
```yaml
resourcePolicy:
    - Effect: Deny
      Principal: "*"
      Action: execute-api:Invoke
      Resource:
        - execute-api:/*/*/forward
      Condition:
        NotIpAddress:
          aws:SourceIp:
            - 192.30.252.0/22
            - 185.199.108.0/22
            - 140.82.112.0/20
    - Effect: Allow
      Principal: "*"
      Action: execute-api:Invoke
      Resource:
        - execute-api:/*/*/forward
      Condition:
        IpAddress:
          aws:SourceIp:
            - 192.30.252.0/22
            - 185.199.108.0/22
            - 140.82.112.0/20
```

If you don't need the usage plans and api key part, remove this part by following the article.

After this, make a Serverless install
```
sls install
```

And deploy with:
```
sls deploy
```

