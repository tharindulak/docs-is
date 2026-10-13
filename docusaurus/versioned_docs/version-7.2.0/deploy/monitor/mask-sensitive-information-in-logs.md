---
title: Mask Sensitive Information in Logs
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/deploy/monitor/mask-sensitive-information-in-logs.md
---

# Mask Sensitive Information in Logs

There can be business-sensitive information that is added to logs in the product console and/or Carbon log files. When these logs are analyzed, the information is exposed to those who check them.

To avoid this potential security pitfall, users can mask sensitive information.

## Mask Sensitive Information in Logs with Log4j

Users can mask sensitive information from the log file at the time of logging. In this feature, you can define patterns that need to be masked from the logs. This is particularly useful in the cases of credit card numbers, access tokens, etc.

For more information, refer to [Configure log masking with Log4j](log4j-mask-sensitive-information-in-logs.md)

## Mask Sensitive Information in Logs with Filebeat

Users can mask sensitive information from the logs at the time of shipping with Filebeat.
In this feature, you can define patterns that need to be masked from the logs and it will be masked at the Filebeat level and shipped. However, the log file itself will contain sensitive information.

For more information, refer to [Configure log masking with Filebeat](elk-mask-sensitive-information-in-logs.md)
