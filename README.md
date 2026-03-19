# Winter Weather Route Optimizer API

## Introduction

The Winter Weather Route Optimizer API empowers Foomatic's route planning engine to handle complex delivery and sales routes across rural and prairie regions during winter months. By integrating real-time road condition data and weather hazard alerts, the API enables automatic rerouting of multi-day and multi-week delivery plans away from impassable roads and active blizzard zones. This enhancement ensures driver safety, maintains realistic delivery windows for customers, and protects Foomatic's reputation as a reliable logistics partner with critical capabilities as the company expands.

## Endpoints and parameters

To provide comprehensive coverage for our dispatch teams, this API utilizes two primary `GET` endpoints:

1. `/routes/plow-status`: This endpoint queries provincial and municipal databases to determine if a specific rural road has been cleared of snow. 
2. `/routes/ice-warnings`: This endpoint checks for active black ice or freezing rain advisories along a specified path.

Because we are utilizing two endpoints, they share two required parameters to accurately process the routing logic:
* `highway_number` (string): The designated alphanumeric code for the road or highway (e.g., "QH-1").
* `vehicle_traction_type` (string): The current equipment profile of the Foomatic delivery truck (e.g., "winter-tires" or "chains").

## Resources

When the Foomatic routing engine queries the API, it receives a lightweight JSON object designed for quick parsing by our automated systems. 

The primary resource returned contains three properties: a `safe_to_travel` boolean indicating if the route is passable, an `estimated_weather_delay_minutes` integer to help management adjust customer delivery windows, and a brief `recommendation` string providing specific instructions for the driver.

## Example

**Request:**
```
GET /routes/plow-status?highway_number=QH-1&vehicle_traction_type=winter-tires
```

**Response:**
```json
{
  "safe_to_travel": true,
  "estimated_weather_delay_minutes": 15,
  "recommendation": "Proceed with caution"
}
```
