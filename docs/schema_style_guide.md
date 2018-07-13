# The Human Cell Atlas: Metadata Schema Style Guide

## Table of Contents
- [Introduction](#introduction)
- [Schema formatting](#schema-formatting)
- [Field formatting](#field-formatting)
- [General rules](#general-rules)

## Introduction

This document describes the style and formatting rules followed when evolving the HCA metadata standard.

**What is in this document**
- General style guidelines and formatting for metadata schema and fields

**Who should be reading this document?**
- HCA DCP internal developers
- Anyone reporting a bug in the schema
- Members of external projects seeking alignment with HCA metadata standards

**What *isn't* in this document?**
- Directions for [requesting or suggesting changes](metadata-schema/docs/contributing.md) to the metadata schema
- Directions for [making changes to metadata schemas](metadata-schema/docs/committers.md)

## Schema formatting


## Field formatting

### Required field attributes

The following attributes are required for each metadata field in an HCA metadata schema. 

1. **description:** A clear, concise statement of the what the metadata field is. The *description* value will appear in the metadata spreadsheet and be displayed in the Metadata Dictionary on the Data Portal. 

    Example:

        "email": {
            "description": "Email address for the individual.",
            ...
        }

    Each *description* should be one or more phrases or sentences and end in a full stop (period).

1. **type:** The JSON type of value required for the metadata field. The *type* value will be displayed in the Metadata Dictionary on the Data Portal.

    Example:
    
        "email": {
            "description": "Email address for the individual.",
            "type": "string",
            ...
        }
        
    Example valid *type* values include: string, number, boolean, array (when a field is an array of values), and object (when a field references another schema). The specification of valid JSON *type* values can be found [here](http://json-schema.org/latest/json-schema-validation.html#rfc.section.6.1.1). 

1. **example:** Directions for how to enter a valid value in the metadata field and/or an example valid value. The *example* value will appear in the metadata spreadsheet and be displayed in the Metadata Dictionary on the Data Portal. 

    Examples:
    
        "email": {
            "description": "Email address for the individual.",
            "type": "string",
            "example": "Enter a valid email address.",
            ...
        },

        "project_role": {
            "description": "Primary role of the individual in the project.",
            "type": "string",
            "example": "principal investigator",
            ...
        }

    Sometimes including an *example* value is not necessary, including:
    
    - When a field imports a core or module schema (e.g. `donor_organism.medical_history`) because the core and module schema fields will have their own examples
    - When including an example for the field could bias data contributors (e.g. `donor_organism.biomaterial_id`) 

1. **user-friendly:** A user-facing, readable term/phrase of what the metadata field is. The *user-friendly* value will appear in the metadata spreadsheet, be displayed in the Data Browser, and be displayed in the Metadata Dictionary on the Data Portal. 

    Example:
    
        "email": {
            "description": "Email address for the individual.",
            "type": "string",
            "example": "Enter a valid email address.",
            "user_friendly": "Email address",
            ...
        },

    Including *user-friendly* values for metadata fields has many advantages, including: 
    
    1. Unlike the actual metadata field name, the *user-friendly* value can contain punctuation, spaces, capitalization, and other basic formatting to make the interpretation of the field easier for data contributors and consumers.
    1. Updates or changes to a *user-friendly* value are considered a patch increment to the schema version number and are thus easier and simpler to implement than metadata field name changes.
    1. The *user-friendly* values can be templated to allow concatenation of the schema name to the field name for improved clarity. For example, if the *user-friendly* value of the `biomaterial_id` field is set to "${schema} ID", then `donor_organism.biomaterial_id` will render as "Donor ID" while `cell_line.biomaterial_id` will render as "Cell line ID".

### Conditional required field attributes

1. **$ref:** Relative path to a core, module, or ontology schema which is imported by the metadata field. This attribute is required when a field imports a module, core, or ontology schema. The *$ref* value is not displayed to users outside of the JSON schema itself and should always be used with `"type": "object",`.

    Examples:

        "project_core" : {
            "description": "Core project-level information.",
            "type": "object",
            "$ref": "core/project/project_core.json",
            ...
        },
        "umi_barcode": {
            "description": "Information about unique molecular identifier (UMI) barcode sequences.",
            "type": "object",
            "$ref": "module/process/sequencing/barcode.json",
            ...
        },
        "organism_age_unit": {
            "description": "The unit in which age is expressed.",
            "type": "object",
            "$ref": "module/ontology/time_unit_ontology.json",
            ...
        }

1. **format:** A JSON-defined format that the value supplied to the metadata field should follow. This attribute is required when a field should follow and validate against standard JSON format.

    Example:
    
        "email": {
            "description": "Email address for the individual.",
            "type": "string",
            "example": "Enter a valid email address.",
            "user_friendly": "Email address",
            "format": "email"
        }

1. **enum:**

## General rules

### Tone

1. Avoid using "you" phrases (what is the name of this tone??). For example:

    Bad: `"description": "Your email address."`
    
    Good: `"description": "Email address for the individual."`

1. Avoid making demands. For example:

    Bad: `"description": "You need to include the age of the donor."`
    
    Good: `"description": "Age of the donor."`
    
1. Avoid using "please". For example:

    Bad: `"description": "Please include the phone number of the individual or their lab."`
    
    Good: `"description": "Phone number of the individual or their lab."`

### 