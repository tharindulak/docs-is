---
title: Access the ELK Analytics Dashboard
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/guides/analytics/elk-analytics/accessing-the-analytics-dashboard.md
---

# Access the ELK Analytics Dashboard

Once you have [setup ELK analytics dashboards](../../../deploy/elk-analytics-installation-guide.md), follow the guide below to learn how to access the analytics dashboard.

1. Access Kibana using the following URL:
    <code>http://\{KIBANA_HOST\}:5601</code>

    ![Kibana login](../../../../../assets/img/elk-analytics/accessing-analytics-dashboard/accessing-analytics-dashboard-1.png)

2. You can login to Kibana with the default `elastic` user or refer to the [elastic documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/users-command.html) and learn how to create a new user.

3. On the left panel, navigate to **Analytics** > **Dashboard** and click on **Auth Dashboard**.

    ![Kibana dashboard](../../../../../assets/img/elk-analytics/accessing-analytics-dashboard/accessing-analytics-dashboard-2.png)

4. Use the filter to set the time range in which to view the statistics and click **Update**.

    ![filter auth dashboard](../../../../../assets/img/elk-analytics/accessing-analytics-dashboard/accessing-analytics-dashboard-5.png)

5. To synchronize analytics automatically:
    1. Click the calendar icon in the time range filter.
    2. Toggle **Refresh every** at the bottom of the dropdown.
    3. Set your desired time interval.

        ![synchronize alerts periodically](../../../../../assets/img/elk-analytics/accessing-analytics-dashboard/accessing-analytics-dashboard-6.png)

6. You can use the following filters to narrow down your analytics further.

    ![narrow the search using filters](../../../../../assets/img/elk-analytics/accessing-analytics-dashboard/accessing-analytics-dashboard-7.png)


## What's Next?

Explore the following topics:

- [Analyze Login Attempts](/identity/7.0.0/guides/analytics/analyzing-login-attempts/)
- [Analyze Session Statistics](/identity/7.0.0/guides/analytics/analyzing-active-sessions/)
