Pick one of three projects!
==========================
You can build one of these:
  - Car Rental (includes hierarchy via a self-referencing model, woooo!)
  - Banking (perhaps the simplest of the three)
  - Medical (tracks doctor's appointments and prescriptions)

To get started
==============

```padrino g project ____ -d activerecord -a postgres -t rspec -e haml```

All three of these require these models:
========================================

    padrino g model User name email password_digest phone
    padrino g model Role name
    padrino g model UserRole user:references role:references

In addition, here's the details and extra models for each of these:

Car Rental
==========
Track car categories with a model that is hierarchical, i.e. it references itself.  Top-level categories could be compact, mid-sized, luxury, and van.  Under luxury could be sports cars.  Under mid-sized could be hybrid.  Here's how to build this:

```padrino g model Category name parent:references```

And then in the Category model:
    has_many :children, class_name: "Category", foreign_key: :parent_id, inverse_of: :parent
    belongs_to :parent, class_name: "Category", foreign_key: :parent_id, inverse_of: :children

From there, you need to track which category each car belongs to, and also store year, make, and model information.

Track rentals for each car including pick-up time, drop-off time, starting and ending mileage, fuel level upon return, the customer, the employee at the pick-up counter, and the employee responsible when the car was turned in.

Banking
=======
Track bank accounts based on an account type that includes:
  - name
  - monthly fee
  - overdraft charges
  - interest
  - if it is a checking account
  - if it is a business account

Track accounts that are of a certain account type, and reference the employee who set up the account, and the customer themselves.

Track transactions for each account with a boolean flag if it's a debit or credit, the amount of the transaction, if it was performed at an ATM, the notes for the transaction, and the "work date" (effective date) of the transaction.

Medical
=======
Track doctors, nurses, and patients.

Nurses and doctors can have appointments with patients, while only doctors can make prescriptions for patients.

Track appointments including the scheduled arrival, actual arrival, and appointment duration.  Include the patient and either a nurse or doctor.

Track medications, to only include the name of the medication.

Track prescriptions, to include the patient, prescribing doctor, medication, dosage, and frequency.
