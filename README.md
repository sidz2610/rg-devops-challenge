# Recogizer DevOps/Cloud Engineer Technical Challenge

## Challenge Overview

Welcome to the DevOps/Cloud Engineer technical challenge! In this challenge, you will be tasked with setting up a monitoring and alerting system for a Dockerized environment using Prometheus and Grafana. 

The provided Docker Compose setup includes [Caddy](https://caddyserver.com/docs/) as a reverse proxy and a dummy HTTP service that simulates a web application. More information on this, can be read on the [Services](#services) section below

## Instructions

1. Clone this repository.
2. Create a new branch using the format: `challenge/<name>_<lastname>`.
3. Configure Prometheus and Grafana to monitor the metrics exported by Caddy.
4. Design and create Grafana dashboards that you believe are relevant to monitor the health and performance of the system.
5. Set up alerts in Grafana based on metrics that you deem important for proactive monitoring.
6. Document your solution comprehensively, keeping in mind that in this simulated scenario, the documentation will be used by the DevOps team to understand the dashboards and alerts. For guidance look at the [Documentation](#documentation) section below.
7. Optionally, you can make improvements to the existing Docker Compose file, the provided bash script, or any other components if you find it necessary.

## What is provided ?

- `docker-compose.yml`: Contains the setup with Caddy as a reverse proxy and the dummy HTTP service.
- `Caddyfile`: Configuration file for the caddy service
- `make_requests.sh`: A bash script that allows sending multiple requests to the dummy service to test the dashboards. More on the [Services](#services) section below


## Submission

1. Push all your changes to the branch you created.
2. Provide clear instructions on how to recreate your solution locally.


## Documentation

Please document your solution thoroughly. Consider including the following:

1. **Configuration Steps:**
   - Steps to set up Prometheus and Grafana.
   - Any additional tools or configurations you deemed necessary.

2. **Grafana Dashboards:**
   - Screenshots or snippets of your Grafana dashboards.
   - Explanation of the metrics displayed and their significance.

3. **Alerting Rules:**
   - Description of the alerts you set up in Grafana.
   - Thresholds and conditions for triggering alerts.

4. **Optional Improvements:**
   - If you made enhancements to the Docker Compose file or other components, explain the reasoning behind them.


## Services

### Caddy

[Caddy](https://caddyserver.com/docs/) is a faster and more secure alternative to NGINX. It can be used as web server, reverse proxy and many other cases. 

Configuration is done via a `Caddyfile` (which is also provided). 

This instance of caddy is configured to expose prometheus metrics in port `2019` under `/metrics`

### Dummy HTTP Service

The HTTP Dummy Service is designed for testing and development, responding to every GET request with a specified HTTP status code provided in the 'status' URL parameter. The docker container exposes by default port `8080`

Example usage:

- `curl http://localhost:8080/?status=200`
- `curl http://localhost:8080/?status=404`
- `curl http://localhost:8080/?status=500`

The service will then reply with the given status code and a standard message:

```
Response with status code: <STATUS_CODE>
```

### make_requests.sh

This Bash script works to test the dummy service. It makes multiple HTTP requests to a specified URL with a desired status and a specified time to sleep between requests.

#### Usage

1. Make the script executable:

```bash
chmod +x make_requests.sh
```

2. Run the script with the following arguments:

```bash
./make_requests.sh <URL> <desired_status> <sleep_time>
```
where

- `<URL>`: The URL of the dummy service (or load balancer).
- `<desired_status>`: The desired HTTP status code to include in the requests.
- `<sleep_time>`: Time to sleep between each request in seconds.



#### Example
With the current setup in the docker compose, once that is working the script can run with: 

```bash
./make_requests.sh http://localhost:8080 200 0.5
```

This example runs the script to make requests to the service with a desired status of 200 and a sleep time of 0.5 seconds between requests.

Feel free to customize the parameters according to what you want to test.


## Additional Notes

- Feel free to reach out if you have any questions or need clarification.
- We appreciate clean and well-documented code and configurations.



Good luck, and we look forward to reviewing your solution!
