## 1. Project Link

Project repository / exported Mendix package:

Mendix Version 11.11.0
`https://github.com/vineethk10/Mendix_React_Assessment`

---

## 2. Setup Instructions

1. Open the project in Mendix Studio Pro.
2. Run the app locally.
3. Open the **Work Order Overview** page.

Main buttons available:

* **New**
* **Geocode Selected - API**
* **Generate 100k Test Data**
* **Start Batch Process**
* **Retry Failed** — visible but not implemented
* **Widget**

---

## 3. What I Built

I built a simple **Work Order** sample app.

The main entity is `WorkOrder`.

The app supports:

* Creating work orders
* Updating work orders
* Calling a REST API to geocode an address
* Generating large test data
* Processing work orders in batches
* Displaying work order locations on a map widget
* Tracking batch execution through a batch page

I also added a `BatchJob` entity to show batch progress, including total records, processed count, failed count, status, start time, and completed time.

---

## 4. How to Run or Test

1. Go to **Work Order Overview**.
2. Click **New** and create a work order.
3. Enter title, address, priority, and status.
4. Save the record and confirm it appears in the grid.
5. Select a record and click **Geocode Selected - API**.
6. Confirm latitude and longitude are populated.
7. Click **Generate 100k Test Data** to generate test work orders.
8. Click **Start Batch Process** to process records in batches.
9. Open the **Batch Job Overview** page to check batch progress.

---

## 5. Create and Update Flow

Users create records from the **New** button.

The create flow:

* Creates a new `WorkOrder`
* Sets default values
* Opens the edit page
* Saves the record after validation

Users update records directly from the overview/edit page.

Editable fields include:

* Title
* Description
* Status
* Priority
* Address
* Latitude
* Longitude

---

## 6. REST API Used

I used the **Google Geocoding API**.

Endpoint:

`https://maps.googleapis.com/maps/api/geocode/json`

The app sends the work order address and receives latitude and longitude.

Mapped JSON path:

`results[0].geometry.location.lat`

`results[0].geometry.location.lng`

These values are saved into:

* `WorkOrder.Latitude`
* `WorkOrder.Longitude`

For the map widget, I used the Google Maps JavaScript API:

`https://maps.googleapis.com/maps/api/js`

The widget uses latitude and longitude from the selected work order to show a map pin.

---

## 7. 100,000-Record Batch Processing

The **Generate 100k Test Data** button creates large sample data.

The app does not generate or process all records in one synchronous UI action.

Instead:

* A `BatchJob` record is created.
* Records are generated in chunks.
* The batch size is controlled through batch logic.
* Progress is updated in the `BatchJob` record.
* The Batch Job page shows status and progress.

The **Start Batch Process** button processes work orders in batches.

Basic processing logic:

* Retrieve a limited number of `New` work orders.
* Mark each record as processed.
* Set processed date and external reference.
* Track processed and failed counts.
* Update the batch job status.

This shows awareness of chunking, transaction boundaries, and avoiding long-running UI actions.

---

## 8. Batch Page

I added a **Batch Job Overview** page to monitor background work.

The page shows:

* Job type
* Status
* Total records
* Processed count
* Failed count
* Batch size
* Started on
* Completed on
* Last error

This gives visibility into large data generation and processing.

---

## 9. Known Limitations

* Retry Failed button is added but not implemented.
* Error handling is basic.
* No advanced audit history.
* No dead-letter queue.
* No advanced monitoring or alerting.
* Google API key configuration is basic for demo purposes.
* The map widget shows basic pin functionality only.
* The app should not render 100,000 map pins at once.

---

## 10. Improvements With More Time

With more time, I would add:

* Full retry failed implementation
* Retry count handling
* Failed record reprocessing
* Batch chunk tracking
* Better error handling
* API rate-limit handling
* Audit history
* More secure API key management
* Automated tests
* Improved map widget with clustering and better marker styling

---
