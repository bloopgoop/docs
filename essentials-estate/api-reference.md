---
title: API Reference
layout: default
parent: Essentials Estate
nav_order: 3
---

# API Reference
{: .fs-9 }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## User APIs - prefix `api`

### /
{: .text-purple-000}

`GET`

returns a list of routes

<ins>Inputs</ins>

<dl>
<dd>None</dd>
</dl>

<ins>Returns</ins>

<dl>
<dd>A list of routes</dd>
</dl>

### /token/
{: .text-purple-000}

`POST`

authenticates user and returns a JSON web token

<ins>Inputs</ins>

<dl>
<dd>username</dd>
<dd>password</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> refresh and access JSON web token</dd>
<dt>On fail</dt>
<dd><code>400, 401</code> None</dd>
</dl>

### /token/refresh/
{: .text-purple-000}

`POST`

takes a refresh token and returns a new JSON web token

<ins>Inputs</ins>

<dl>
<dd>refresh</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> refresh and access JSON web token</dd>
<dt>On fail</dt>
<dd><code>400, 401</code> None</dd>
</dl>

### /register/
{: .text-purple-000}

`POST`

registers an account with the system, users will get a confirmation email to finish the signup process

<ins>Inputs</ins>

<dl>
<dd>first_name</dd>
<dd>last_name</dd>
<dd>username</dd>
<dd>email</dd>
<dd>password</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>201</code> Response("Click the link in your email to activate the account")</dd>
<dt>On fail</dt>
<dd><code>500</code> None</dd>
</dl>

### /activate/{uidb64}/{token}/
{: .text-purple-000}

`GET`

confirms the user's email and finishes the signup process

<ins>Inputs</ins>

<dl>
<dd>None</dd>
</dl>

<ins>Returns</ins>

<dl>
<dd>None</dd>
</dl>

### ~~/users/payment/~~
{: .text-purple-000}

`POST`

<ins>Returns</ins>

<dl>
<dd>None</dd>
</dl>

## Property APIs - prefix `property`

### /
{: .text-purple-000}

`GET, POST`

#### GET
{: .text-purple-000}

gets properties in range [start, end], if not specified, get first 50

<ins>URL params</ins>

<dl>
<dt>start?</dt>
<dt>end?</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> list of properties</dd>
<dt>On fail</dt>
<dd><code>500</code> None</dd>
</dl>

#### POST
{: .text-purple-000}

saves a property to user's account

<ins>Inputs</ins>

<dl>
<dd>address</dd>
<dd>city</dd>
<dd>state</dd>
<dd>zip</dd>
<dd>title</dd>
<dd>rent</dd>
<dd>description</dd>
<dd>bedrooms</dd>
<dd>bathrooms</dd>
<dd>garage</dd> 
<dd>sqft</dd>
<dd>lotsize</dd>
<dd>type</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> new property id</dd>
<dt>On fail</dt>
<dd><code>500</code> None</dd>
</dl>

### /{id}/
{: .text-purple-000}

`GET, PUT, DELETE`

#### GET
{: .text-purple-000}

saves a property to user's account

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>Property with corresponding id</dd>
<dt>On fail</dt>
<dd><code>500</code> None</dd>
</dl>


#### PUT
{: .text-purple-000}

edit a property if owned by user

<ins>Inputs</ins>

<dl>
<dd>address</dd>
<dd>city</dd>
<dd>state</dd>
<dd>zip</dd>
<dd>title</dd>
<dd>rent</dd>
<dd>description</dd>
<dd>bedrooms</dd>
<dd>bathrooms</dd>
<dd>garage</dd> 
<dd>sqft</dd>
<dd>lotsize</dd>
<dd>type</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> None</dd>
<dt>On fail</dt>
<dd><code>404</code> None</dd>
</dl>

#### DELETE
{: .text-purple-000}

deletes a property if owned by user

<ins>Inputs</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> None</dd>
<dt>On fail</dt>
<dd><code>404</code> None</dd>
</dl>

### /userProperty/
{: .text-purple-000}

`GET`

gets a list of all the user's properties

<ins>Inputs</ins>

<dl>
<dd>None</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> list of user's properties</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>

### /photo/
{: .text-purple-000}

`POST`

Adds photos to a property

<ins>Inputs</ins>

<dl>
<dd>files</dd>
<dd>descriptions</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> None</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>

### /photo/delete/
{: .text-purple-000}

`DELETE`

deletes photos from a property

<ins>URL params</ins>

<dl>
<dt>photoIDs</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code> None</dd>
<dt>On fail</dt>
<dd><code>403, 400</code> None</dd>
</dl>

### /rating/{id}/
{: .text-purple-000}

`GET, POST, PUT, DELETE`

#### GET
{: .text-purple-000}

returns the ratings of a property

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>list of ratings</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>


#### POST
{: .text-purple-000}

creates a rating on a property and returns it

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Inputs</ins>

<dl>
<dd>stars</dd>
<dd>comment</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>new rating</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>

#### PUT
{: .text-purple-000}

edits a rating on a property

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Inputs</ins>

<dl>
<dd>stars</dd>
<dd>comment</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>None</dd>
<dt>On fail</dt>
<dd><code>401, 404</code> None</dd>
</dl>

#### DELETE
{: .text-purple-000}

deletes a rating on a property

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>None</dd>
<dt>On fail</dt>
<dd><code>401, 404</code> None</dd>
</dl>

### /reviewProperty/{admin}/
{: .text-purple-000}

`GET, POST`

#### GET
{: .text-purple-000}

<ins>URL params</ins>

<dl>
<dt>admin</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>list of user's properties if admin == 0, list of all properties if admin == 1</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>

#### POST
{: .text-purple-000}

<ins>URL params</ins>

<dl>
<dt>admin</dt>
</dl>

<ins>Inputs</ins>

<dl>
<dd>propertyID</dd>
<dd>status</dd>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>list of all properties in review</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>


### /requestRental/{id}/
{: .text-purple-000}

`GET, POST`

#### GET
{: .text-purple-000}

returns the status of the rental request for the given property

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>status of rental request for given property</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>

#### POST
{: .text-purple-000}

Makes a requestRental object with the given propertyID and the user

<ins>URL params</ins>

<dl>
<dt>id</dt>
</dl>

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>rental status</dd>
<dt>On fail</dt>
<dd><code>400, 500</code> None</dd>
</dl>

### /getRequest/
{: .text-purple-000}

`GET`

returns all properties with a rentalRequest object associated with user

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>list of properties that user has requested a rental for</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>
</dl>

### /user/
{: .text-purple-000}

`GET`

gets user's data

<ins>Returns</ins>

<dl>
<dt>On success</dt>
<dd><code>200</code>user data</dd>
<dt>On fail</dt>
<dd><code>400</code> None</dd>