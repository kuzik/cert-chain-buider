# Cert chain builder

Project provides functionality for generating ssl chains from the .json file


## Example
Input
```json
[
  {
    "common_name": "Root CA",
    "type": "root",
    "organization": "My Organization",
    "country": "US",
    "validity": {
      "start_date": "2024-01-01",
      "end_date": "2034-01-01"
    },
    "key_size": 4096,
    "children": [
      {
        "common_name": "Intermediate CA 1",
        "type": "ica",
        "organization": "My Organization",
        "country": "US",
        "validity": {
          "start_date": "2024-01-01",
          "end_date": "2030-01-01"
        },
        "key_size": 2048,
        "children": [
          {
            "common_name": "www.example.com",
            "type": "ee",
            "organization": "Example Corp",
            "country": "US",
            "validity": {
              "start_date": "2024-01-01",
              "end_date": "2026-01-01"
            },
            "key_size": 2048,
            "children": []
          }
        ]
      },
      {
        "common_name": "Intermediate CA 2",
        "type": "ica",
        "organization": "My Organization",
        "country": "US",
        "validity": {
          "start_date": "2024-01-01",
          "end_date": "2030-01-01"
        },
        "key_size": 2048,
        "children": []
      }
    ]
  }
]
```

Output
- **root_ca**
    - Root CA.pem
    - Root CA.key
    - **Intermediate CA 1**
        - Intermediate CA 1.pem
        - Intermediate CA 1.key
        - **www.example.com**
            - www.example.com.pem
            - www.example.com.key
    - **Intermediate CA 2**
        - Intermediate CA 2.pem
        - Intermediate CA 2.key
