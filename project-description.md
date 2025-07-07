# Test Project Outline – Module D – Lyon Mobile Web Service

## Competition time

3 hours

## Introduction

In this project, you will create a mobile web application that provides access to essential service data for the city of Lyon. The application dynamically retrieves data from a mock API server, which is pre-built and supplied to you.

## General Description of Project and Tasks

The task involves developing a mobile-first web application that fetches and displays service-related information for Lyon. The data is retrieved dynamically through the provided API. The application includes multiple views for carpark availability, local events, weather forecasts, and user settings. It must support fixed-position header and navigation bars, both vertical and horizontal scrolling, and interactive features such as sorting, pinning, filtering, and animated SVG rendering. The app should utilize local storage where appropriate and ensure accessibility and compatibility with mobile platforms.

To run the API server in a Dockerized environment, navigate to `/assets/mock-api-server` and execute `docker-compose up -d` . Once started, the mock server will be accessible at [http://localhost:5555](http://localhost:5555).

## Requirements

### Mobile Web Layout

- The layout consists of a header bar, a main content area, and a navigation bar.
- The header bar remains fixed at the top of the screen.
- The navigation bar remains fixed at the bottom of the screen.
- When the content overflows, only the main content area should scroll.
- The header may show the current view title and include a back-navigation option.

### Navigation Bar

The navigation bar must include the following four buttons:

1. Carparks
2. Events
3. Weather
4. Setting

### Data API

Data should be retrieved from the following endpoints:

- `/carparks`
- `/events`
- `/weather`

### Paging

- The events API supports pagination, indicated via a `pages` object that includes `next` and `prev` URLs.
- Example: `/events?page=2`
  ```json
  {
    "events": [
      {
        "title": "Jazz & Wine: Lyon Jazz & Wine Festival",
        "image": "/image.png?title=Jazz %26 Wine: Lyon Jazz %26 Wine Festival",
        "date": "2025-10-17"
      }
      ...
    ],
    "pages": {
      "next": "/events?page=3",
      "prev": "/events?page=1"
    }
  }
  ```

### Carpark Availability

- Display a list of carparks, each showing availability counts.

#### Sorting

- Provide a toggle (in the settings view) to sort carparks:
  - Alphabetically
  - By distance from the current location

#### Geolocation

- Default behavior: attempt to access the user's current geolocation.
- If geolocation access is blocked due to competition environment restrictions, the implementation will be reviewed in the source code.
- Geolocation can also be simulated via URL query parameters: `?latitude=45.755051&longitude=4.846358`
- Use the provided JavaScript code to calculate distances.

#### Focusing on a Carpark

- When a user selects a carpark, display only its name, distance, and availability.
- Provide a way to return to the full list.

#### Pinning Carparks

- Users can pin or unpin carparks to appear at the top of the list, regardless of the sort method.
- Pinned state must be saved in `localStorage` and persist on page reload.

### Lyon Events

- Initially display events as returned by the default API.
- Each event should show an image, title, and date.

#### Filtering by Date

- Provide date inputs for specifying a beginning and/or ending date.
- Use the following URL pattern for filtering: `/module_d_api.php/events.json?beginning_date=YYYY-MM-DD&ending_date=YYYY-MM-DD`

#### Infinite Scrolling

- Automatically load more events as the user scrolls to the bottom of the list.
- Infinite scrolling must:
  - Avoid duplicate or missing entries
  - Load new items smoothly and at the appropriate time (not too early or late)

### Weather

- Display a 7-day weather forecast.

#### Horizontal Scrolling

- Weather data should be presented horizontally.
- Enable scroll snapping to align each day's forecast with the viewport.
- Refer to the provided visual mockup.

![Horizontal scrolling](/assets/project-description-images/horizontal-scrolling.png)

#### SVG Icons

- Display SVG icons for each day based on API-provided weather status.
- On mouse hover, apply animated stroke effects:
  - Stroke color: `#1c3e60`, width: 1, fill: none
  - Animate `stroke-dasharray` from 50 to 200 over 2 seconds
  - Animate `stroke-dashoffset` from 200 to 0
- Refer to `svg-icon-animation.mp4` in the media folder

### Settings View

- Accessible through the fourth button in the navigation bar.

#### Theme Configuration

- Allow the user to select among:
  - Light theme
  - Dark theme
  - System-default theme

#### Carpark Sorting Method

- Include a toggle for choosing the carpark sorting method:
  - Alphabetical
  - By distance

### Mobile Web App Configuration

- Include a `manifest.json` file and relevant meta tags for Android and iOS support.
- Ensure the viewport is configured for optimal mobile viewing.

### Accessibility

- Ensure good accessibility practices.
- The project will be evaluated using Chrome Lighthouse's accessibility score.
- JavaScript code should be clean and easy to maintain.

## Assessment

Evaluation will be conducted using **Google Chrome**.&#x20;

## Mark Distribution

| WSOS SECTION | Description        | Points |
| ------------ | ------------------ | ------ |
| 1            | Mobile Web General | 2.5    |
| 2            | Carpark            | 3.0    |
| 3            | Events             | 3.25   |
| 4            | Weather            | 1.75   |
| 5            | Settings & General | 2.25   |
| **Total**    |                    | 12.75  |
