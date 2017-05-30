**Anki-MedRec Platform - External APIs**
===================


This page describes the APIs that are required as part of **v1**.


----------


Physician
-------------

Physician is the person qualified to practise medicine, especially one who specialises in diagnosis and medical treatment.

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Full Name
- Medical speciality
- Prescriptions
- Calendar
- Availability for appointment

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "Id": "Physician Id",
  "FullName": "Physician Full Name",
  "MedicalSpeciality": "Physician speciality",
  "Prescriptions": [
    {
      "Id": "Prescription Id",
      "Name": "Prescription Name",
      "PatientId": "Patient Id",
      "Notes": "Prescription notes",
      "Drugs": [
        {
          "Id": "Drug Id",
          "Name": "Drug Name",
          "Formula": "Drug Formula",
          "SideEffects": [
            {
              "Name": "Side effect name",
              "Description": "Side effect description"
            }
          ]
        }
      ]
    }
  ],
  "Calendar": [
    {
      "Name": "Meeting name",
      "StartTime": "2017-05-22T02:21:05+00:00",
      "Duration": "1h"
    }
  ],
  "Availability": [
    {
      "AvailabilityStartTime": "2017-05-22T02:21:05+00:00",
      "Duration": "1h"
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing physician(s)
<br>
> **/physicians** --`It returns the full list of physicians with all required attributes`
<br>
> **/physician/{id}**   -- `It returns the list of required attributes for this physician.`
<br>
> **/physician/{id}/agenda** -- `It returns the next 2 weeks agenda.`
<br>
> **/physician/{id}/availability**  -- `It returns the next 2 weeks availability.`
<br>
> **/physician/{id}/prescriptions**  -- `It returns the full list of prescriptions issued by this physician.`
<br>

- **PUT** -- Updates existing physician(s)
> **/physician**   -- `JSON payload expected with all physician's attributes attached, including Id.`

- **POST** -- Creates new physician(s)
> **/physicians** -- `JSON payload expected with list of physicians attributes attached.`
<br>
> **/physician**   -- `JSON payload expected with physician's attributes attached.`

- **DELETE** -- Delete existing physician(s)
> **/physician/{id}**   -- `Deletes Physician by Id.`

 
<br>

Patient
-------------

Patient is a person receiving or registered to receive medical treatment.

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Full Name
- Age
- Address
- Mobile
- Email
- Medical Conditions `-- See "Medical Conditions"`
- Medical Appointments `-- See "Appointments"`
- Prescriptions `-- See "Prescriptions"`
- Medical measures `-- See "Measures"`

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "Id": "Patient Id",
  "FullName": "Patient Full Name",
  "Age": "Patient Age",
  "Address": "Patient Address",
  "Mobile": "Patient Mobile",
  "Email": "Patient Email",
  "MedicalConditions": [
    {
      "Id": "Medical Condition Id",
      "Name": "Medical Condition Name",
      "Symptoms": [
        {
          "Id": "Symptom Id",
          "Name": "Symptom Name"
        }
      ],
      "Treatment": [
        {
          "Id": "Treatment Id",
          "Name": "Treatment Name"
        }
      ]
    }
  ],
  "MedicalAppointments": [
    {
      "Id": "Appointment Id",
      "Name": "Appointment Name",
      "PhysicianId": "Physician Id",
      "PhysicianName": "Physician Name",
      "AppointmentDate": "2017-05-22T02:21:05",
      "Duration": "1h",
      "Notes": "Appointment Notes"
    }
  ],
  "Prescriptions": [
    {
      "Id": "Prescription Id",
      "Name": "Prescription Name",
      "PhysicianId": "Patient Id",
      "Notes": "Prescription notes",
      "Drugs": [
        {
          "Id": "Drug Id",
          "Name": "Drug Name",
          "Formula": "Drug Formula",
          "SideEffects": [
            {
              "Name": "Side effect name",
              "Description": "Side effect description"
            }
          ]
        }
      ]
    }
  ],
  "MedicalMeasures": [
    {
      "Id": "Measure Id",
      "Name": "Measure Name",
      "Type": "HeartBeat",
      "RecordingDevice": "iHealth|SamsungGear3|Manual",
      "Date": "2017-05-22T02:21:05+00:00",
      "Notes": "Measure Notes"
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing patient(s)
> **/patients** -- `It returns the full list of patients with all required attributes.`
<br>
> **/patient/{id}**   -- `It returns the list of required attributes for this patient.`
<br>
> **/patient/{id}/conditions**  -- `It returns the Patient's Medical Conditions.`
<br>
> **/patient/{id}/appointments** -- `It returns the patient's next 2 weeks appointments.`
<br>
>  **/patient/{id}/prescriptions** -- `It returns the full list of prescriptions issued to this patient.`

- **PUT** -- Updates existing patient(s)
> **/patient**   -- `JSON payload expected with patient's attributes attached, including Id.`

- **POST** -- Creates new patient(s)
> **/patients** -- `JSON payload expected with list of patients attributes attached.`
<br>
> **/patient**   -- `JSON payload expected with patient's attributes attached.`

- **DELETE** -- Delete existing patient(s)
> **/patient/{id}**   -- `Deletes a patient by Id.`

<br>

Appointments
-------------

Medical appointments between a Patient and a Physician in order to undergo a medical procedure.

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Name
- Physician Id
- Patient Id
- Date and Time
- Duration
- Notes

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "MedicalAppointments": [
    {
      "Id": "Appointment Id",
      "Name": "Appointment Name",
      "PhysicianId": "Physician Id",
      "PatientId": "Patient Id",
      "AppointmentDate": "2017-05-22T02:21:05",
      "Duration": "1h",
      "Notes": "Appointment Notes"
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing appointment(s)
> **/appointments** -- `It returns the full list of existing appointments with all required attributes.`
<br>
> **/appointment/{id}**   -- `It returns the list of required attributes for this appointment.`

- **PUT** -- Updates existing appointment(s)
> **/appointment**   -- `JSON payload expected with appointment's attributes attached, including Id.`

- **POST** -- Creates new appointment(s)
> **/appointments** -- `JSON payload expected with list of appointments attributes attached.`
<br>
> **/appointment**   -- `JSON payload expected with appointment's attributes attached.`

- **DELETE** -- Delete existing appointment(s)
> **/appointment/{id}**   -- `Deletes an appointment by Id.`


<br>
 
Prescriptions
-------------

Prescriptions are instructions written by a medical practitioner that authorises a patient to be issued with a medicine or treatment.

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Name
- Physician Id
- Patient Id
- Medical drugs  `See Drugs below`
- Notes

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "Prescriptions": [
    {
      "Id": "Prescription Id",
      "Name": "Prescription Name",
      "PatientId": "Patient Id",
      "Notes": "Prescription notes",
      "Drugs": [
        {
          "Id": "Drug Id",
          "Name": "Drug Name",
          "Formula": "Drug Formula",
          "SideEffects": [
            {
              "Name": "Side effect name",
              "Description": "Side effect description"
            }
          ]
        }
      ]
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing prescription(s)
> **/prescriptions** -- `It returns the full list of issued prescriptions with all required attributes.`
<br>
> **/prescription/{id}**   -- `It returns the list of required attributes for this prescription.`

- **PUT** -- Updates existing prescription(s)
> **/prescription**   -- `JSON payload expected with prescription's attributes attached, including Id.`

- **POST** -- Creates new prescription(s)
> **/prescriptions** -- `JSON payload expected with list of prescriptions attributes attached.`
<br>
> **/prescription**   -- `JSON payload expected with prescription's attributes attached.`

- **DELETE** -- Delete existing prescription(s)
> **/prescription/{id}**   -- `Deletes a prescription by Id.`

<br>
  
Measures
-------------

Patients Medical Measures are a series of constant recordings on a patient's record that help understand pre-existing conditions, diagnosis and potential treatments. Examples of Patient's Medical measures are: weight, temperature, blood pressure, stress level, heart beat, etc.

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Patient Id
- Name
- Type
- Recording device 
- Date of measure
- Notes

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "MedicalMeasures": [
    {
      "Id": "Measure Id",
      "Name": "Measure Name",
      "Type": "HeartBeat",
      "RecordingDevice": "iHealth|SamsungGear3|Manual",
      "Date": "2017-05-22T02:21:05+00:00",
      "Notes": "Measure Notes"
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing patient's medical measure(s)
> **/measures** -- `It returns the full list of measures with all required attributes.`
<br>
> **/measure/patient/{id}**   -- `It returns the list of measures conducted on patient id`

- **POST** -- Creates new patient's medical measure(s)
> **/measures** -- `JSON payload expected with list of full patients list medical measures attached. This API is merely used for maintenance/data recovery purposes.`
<br>
> **/measure/patient/{id}**   -- `JSON payload expected with a new patient medical measure  attached.`

- **DELETE** -- `Delete existing patient's medical measure(s)`
> **/measure/patient/{id}**   -- `Deletes ALL existing patient's medical measures. - This API is merely used for maintenance purposes.`

   
<br>

Drugs
-------------

A pharmaceutical drug (also referred to as medicine, medication, or simply as drug) is a drug used to diagnose, cure, treat, or prevent disease.

    Note: This is just an inventory of Drugs. In order to prescribe drugs, see "Prescriptions"

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Name
- Formula
- Side effects

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "Drugs": [
    {
      "Id": "Drug Id",
      "Name": "Drug Name",
      "Formula": "Drug Formula",
      "SideEffects": [
        {
          "Name": "Side effect name",
          "Description": "Side effect description"
        }
      ]
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing drug(s)
> **/drugs** -- `It returns the full list of existing drugs in the inventory with all required attributes.`
<br>
> **/drug/{id}**   -- `It returns the list of required attributes for this drup.`

- **PUT** -- Updates existing drug(s)
> **/drug**   -- `JSON payload expected with drug's attributes attached, including Id.`

- **POST** -- Creates new drug(s)
> **/drugs** -- `JSON payload expected with list of drugs attributes attached.`
<br>
> **/drug**   -- `JSON payload expected with drug's attributes attached.`

- **DELETE** -- Delete existing drug(s)
> **/drug/{id}**   -- `Deletes an drug by Id.`

<br>

Medical Conditions
-------------

Medical Conditions refer to all diseases, illnesses, and injuries as result of a physical injury.

    Note: This is just a catalogue of Medical Conditions. In order to prescribe treatments, see "Prescriptions".

#### <i class="icon-file"></i> Required attributes:

The list below shows only those attributes that are required for v1.
<br>

- Id
- Name
- Symptoms
- Treatment

#### <i class="icon-file"></i> Sample JSON payload:
    
```json
{
  "MedicalConditions": [
    {
      "Id": "Medical Condition Id",
      "Name": "Medical Condition Name",
      "Symptoms": [
        {
          "Id": "Symptom Id",
          "Name": "Symptom Name"
        }
      ],
      "Treatment": [
        {
          "Id": "Treatment Id",
          "Name": "Treatment Name"
        }
      ]
    }
  ]
}
```

#### <i class="icon-file"></i> Required APIs:

- **GET** -- Get existing disease(s)
> **/diseases** -- `It returns the full list of existing diseases in the catalogue with all required attributes.`
<br>
> **/disease/{id}**   -- `It returns the list of required attributes for this disease.`

- **PUT** -- Updates existing disease(s)
> **/disease**   -- `JSON payload expected with disease's attributes attached, including Id.`

- **POST** -- Creates new disease(s)
> **/diseases** -- `JSON payload expected with list of diseases attributes attached.`
<br>
> **/disease**   -- `JSON payload expected with disease's attributes attached.`

- **DELETE** -- Delete existing disease(s)
> **/disease/{id}**   -- `Deletes a disease by Id.`f



----------

<a href="index" rel="Go back">![link text](./img/back.png "Go Back")</a>

