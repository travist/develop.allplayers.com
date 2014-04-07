---
layout: default
title: WebForms API
---
# Webforms API

* [Get Groups Webforms](#group_webforms)
* [Retrieve Webform](#retrieve)
* [Search Submissions](#submissions)
* [Get Submission](#submission)
* [Create Submission](#create_submission)

<a id="group_webforms"></a>
## Getting a groups webforms

You can get all the group's webforms by going to the following endpoint:

    /groups/{uuid}/webforms [GET]

<pre class="terminal">
$ curl https://www.allplayers.com/api/v1/rest/groups/a429c1ae-7a2b-11e3-8c9b-22000a9b80ff/webforms
{
  12fbf38d-9d7c-11e3-8c9b-22000a9b80fef: Booth Registration Form
  35704401-9d8d-11e3-8c9b-22000a9b80fed: Exhibitor AV Rental Form
}
</pre>

<a id="retrieve"></a>
## Getting webform information

You can get the webform information by going to the following endpoint:

    /webforms/{uuid} [GET]

<pre class="terminal">
$ curl https://www.allplayers.com/api/v1/rest/webforms/006ca0d1-759c-11e2-a02b-22000a929434
{
  uri: >
    https://www.allplayers.com/api/v1/rest/webforms/006ca0d1-759c-11e2-a02b-22000a929434
  uuid: 006ca0d1-759c-11e2-a02b-22000a929434
  title: Example Webform
  description: Example description of webform
  created: 1348925207
  updated: 1390507317
  submissions: >
    https://www.allplayers.com/api/v1/rest/webforms/006ca0d1-759c-11e2-a02b-22000a929434/submissions
  webform:
    components:
      5:
        cid: 5
        form_key: profile__field_email__profile
        name: Email Address
        type: email
      1:
        cid: 1
        form_key: profile__field_firstname__profile
        name: First Name
        type: textfield
      2:
        cid: 2
        form_key: profile__field_lastname__profile
        name: Last Name
        type: textfield
      3:
        cid: 3
        form_key: group_bio_data
        name: Bio data
        type: fieldset
      4:
        cid: 4
        form_key: profile__field_birth_date__profile
        name: Birthday
        type: date
      6:
        cid: 6
        form_key: org__sequential_id__org_webform
        name: Member ID
        type: sequential_id
      7:
        cid: 7
        form_key: profile__field_address__profile
        name: Home Address
        type: fieldset
      8:
        cid: 8
        form_key: profile__field_address_street__profile
        name: Address 1
        type: textfield
      9:
        cid: 9
        form_key: profile__field_address_additional__profile
        name: Address 2
        type: textfield
      10:
        cid: 10
        form_key: profile__field_address_city__profile
        name: City
        type: textfield
      11:
        cid: 11
        form_key: profile__field_address_province__profile
        name: State/Province
        type: select
      12:
        cid: 12
        form_key: profile__field_address_postal_code__profile
        name: Zip
        type: textfield
      13:
        cid: 13
        form_key: profile__field_address_country__profile
        name: Country
        type: select
      14:
        cid: 14
        form_key: group_player
        name: Participant information
        type: fieldset
      15:
        cid: 15
        form_key: profile__field_phone__profile
        name: Phone
        type: textfield
      16:
        cid: 16
        form_key: organization_name
        name: Organization Name
        type: textfield
}
</pre>

<a id="submissions"></a>
## Searching webform submissions information

You can search the webform submissions information by going to the following endpoint:

  /forms/{uuid}/submission [GET]

**Params**

*  `form_keys` Array containing possible fields to filter on.
*  `user_uuid` UUID of user that you want to search and find a submission in the webform.

<pre class="terminal">
$ curl https://www.allplayers.com/api/v1/rest/forms/006ca0d1-759c-11e2-a02b-22000a929434/submission?form_keys[__profile__field_firstname__profile]=Mark&form_keys[__profile__field_lastname__profile]=Fastre
{
sid: 1188
submitted: 1362716988
name: MarkFastre
uuid: a132b459-820d-11e2-a02b-22000a929124
user_uuid: f037329-9be1-11e3-8c9b-22000a9b80fe
}
</pre>

<a id="submission"></a>
## Getting all the submission data

You can retrieve any particular submission:

/submissions/{uuid} [GET]

<pre class="terminal">
$ curl https://www.allplayers.com/api/v1/rest/submissions/5308f9ddb37afa9d7e7324db
{
sid: 891337
uuid: 530829ddb37afa9d7e7324db
uri: >
  https://www.allplayers.com/api/v1/rest/submissions/5308f9ddb37afa9d7e7324db
webform: >
  https://www.allplayers.com/api/v1/rest/webforms/84c37a72-99ae-11e3-8c2b-22000a9b80fe
submitted: 1393097181
data:
  profile__field_firstname__profile: Shawn
  profile__field_lastname__profile: Example
  profile__field_email__profile: ShawnExample@aol.com
  profile__field_birth_date__profile: 1/1/1980
  profile__field_user_gender__profile: Male
  profile__field_school__profile: Example High School
  years_of_service: 9
  niaaa: Yes
  profile__field_id_number_profile: 408
  office: Yes
  member_since: 2005
  profile__field_phone__profile: 412-599-3600 x2405
  work_number: 412-462-3293
  profile__field_home_address_street__profile: 3113 Example Street
  profile__field_home_address_city__profile: Example
  profile__field_home_address_postal_code__profile: 15199
  profile__field_size__profile: L
  profile__field_jacket_size__profile: L
user_uuid: 7f037329-9be1-11e3-8c9b-22000a9b8324
}
</pre>

<a id="create_submission"></a>
## Creating a submission

**Input**

*  `webform`\*
*  `submission[user_uuid]`
*  `submission[data]`\* [info](fields.html#/submission_data)

\* Fields marked with an asterisk are required
Specify either create `POST` or update `PUT`:

You can create submission knowing all the fields from the webform.

  /submissions [POST]

<pre class="terminal">
$ curl -b cjar
https://www.allplayers.com/api/v1/rest/submissions.json
-d"webform=84c37a72-99ae-11e3-8c2b-22000a9b80fe&submission[user_uuid]=7f037329-9be1-11e3-8c9b-22000a9b8324&submission[data][profile__field_email__profile]=testemail@example.com&submission[profile__field_firstname]=testfirstname"
{
  sid: 95820
  uuid: 533c52c47c56f900ed307df2
  uri: >
    https://www.pdup.allplayers.com/api/v1/rest/submissions/533c52c47c56f900ed307df2
  webform: >
    https://www.pdup.allplayers.com/api/v1/rest/webforms/84c37a72-99ae-11e3-8c2b-22000a9b80fe
  submitted: 1396462268
  data:
    profile__field_email__profile: testemail@example.com
    profile__field_firstname__profile: testfirstname
  user_uuid: 7f037329-9be1-11e3-8c9b-22000a9b8324
}
</pre>
