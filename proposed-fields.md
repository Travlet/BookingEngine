# Booking engine voucher integration

> **Note**
> This is a proposed API implementation and is not yet final. We welcome your feedback.

This API is responsible for ingesting booking information, in order to issue Travlet vouchers on the behalf of booking
engines. The API is designed to be easily implemented.

## Endpoint

To communicate with the API webhook, you should use the below API endpoint.

`POST` - `https://travlet.co/api/engine/v1/send`

## Authentication

You will be issued with an API token, which should be sent as a header, named `X-API-TOKEN`.

If the API token is not sent with the request, you will receive a `401 unauthorized` HTTP response.

The API does not currently rate-limit requests.

## Request payload

The table below illustrates the payload required to process the request.

| Name              | Data type | Optional / Required | Information                                                                                                                                     |
|-------------------|-----------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| customer_email    | string    | required            | Email address of the customer. This address is where the voucher code will be sent.                                                             |
| customer_name     | string    | required            | Customer's preferred name. Used to customize email communication with the customer.                                                             |
| hotel_name        | string    | required            | The name of the hotel, or venue where the customer will be staying. Used to customize the email sent to the customer.                           |
| hotel_latitude | string    | required            | Latitude coordinate of the hotel, or venue where the customer will be staying. Used to customize the attraction listings to suggest nearby attractions. |
| hotel_longitude | string    | required            | Longitude coordinate of the hotel, or venue where the customer will be staying. Used to customize the attraction listings to suggest nearby attractions. |
| hotel_id        | mixed    | required            | Booking Engine's internal hotel ID, used for analytics.               |
| booking_created_at        | string    | required            | Timestamp of booking creation. format `YYYY-MM-DD HH:MM:SS`               |
| voucher_id        | string    | optional            | The ID of the voucher that is to be issued to the customer. Required if you provide more than one voucher option to the customer.               |
