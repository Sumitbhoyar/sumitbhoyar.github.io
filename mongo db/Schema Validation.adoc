
# Schema Validation

MongoDB’s collections, by default, does not require its documents to have the same schema.

MongoDB provides the capability to perform schema validation during updates and insertions.

Validation rules are on a per-collection basis.

To specify validation rules when creating a new collection, use db.createCollection() with the validator option.

To add document validation to an existing collection, use collMod command with the validator option.

MongoDB also provides the following related options:

- validationLevel option, which determines how strictly MongoDB applies validation rules to existing documents during an update
   - If the validationLevel is strict (the default), MongoDB applies validation rules to all inserts and updates.
   - If the validationLevel is moderate, MongoDB applies validation rules to inserts and to updates to existing documents that already fulfill the validation criteria. With the moderate level, updates to existing documents that do not fulfill the validation criteria are not checked for validity.

- validationAction option, which determines whether MongoDB should error and reject documents that violate the validation rules or warn about the violations in the log but allow invalid documents.
   - If the validationAction is error (the default), MongoDB rejects any insert or update that violates the validation criteria.
   - If the validationAction is warn, MongoDB logs any violations but allows the insertion or update to proceed.

JSON Schema is the recommended means of performing schema validation.

    db.createCollection( "people" , {
       validator: {
         $jsonSchema: {
            bsonType: "object",
            additionalProperties: false,
    		required: ["name","age"],
            properties: {
               _id : {
                  bsonType: "objectId" },
               name: {
                  bsonType: "string",
                  description: "required and must be a string" },
               age: {
                  bsonType: "int",
                  minimum: 0,
                  maximum: 100,
                  description: "required and must be in the range 0-100" }
            }
         }
    }})

Validation occurs during updates and inserts. When you add validation to a collection, existing documents do not undergo validation checks until modification.
