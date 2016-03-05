**PROBLEM STATEMENT FOR ROR INTERVIEW**
=======================================

**Introduction:**
------------------

Consider a system which support multiple 3rd party delivery api's for smooth functionality. System expects certain input from user. This input is pushed to any available 3rd party api and they return weather they could deliver this package or not along with some other information. This data is later presented to user.

**Your task:**
---------------
Design a system that could scale with any number of 3rd party api's

**Assumptions:**
----------------

 - No two 3rd party api's data and url's would be same.
 - Number of request that needs to be made to 3rd party could vary to complete the
   process.
 - The data that system expect from user has a fixed structure.
 - The data that system shows to user has a fixed structure.

**Examples:**
-------------
**Sample user request and response:**


    Request:
        {
          "name": "Ramesh Yadav",
          "age": "24",
          "items": [
            {
              "name": "cylinder",
              "type": "volatile"
            },
            {
              "name": "ac",
              "type": "non-volatile"
            }
          ],
          "pickup": {
            "house_number": "123",
            "block": "A-Block",
            "locality": "Rajender place",
            "city": "Delhi",
            "State": "Delhi",
            "pincode": "110011"
          },
          "drop": {
            "house_number": "5/2",
            "block": "W-block",
            "locality": "DLF Phase 3",
            "city": "Gurgaon",
            "State": "Haryana",
            "pincode": "122002"
          }
        }
      Response:
        {
          "status": "In Transit",
          "eta": "10 minutes",
          "etd": "60 minutes",
          "cost": "100 Rs."
        }


----------


**Sample api request and response for 3rd party number 1**
  (It return status in response of order placing api)


    POST /order
      Request:
        {
          "customer_name": "Ramesh Yadav",
          "items": [
            {
              "name": "cylinder",
              "type": "volatile"
            },
            {
              "name": "ac",
              "type": "non-volatile"
            }
          ],
          "pickup_address": {
            "house": "123",
            "area": "A-block, Rajender place",
            "city": "Delhi",
            "State": "Delhi",
            "pincode": "110011"
          },
          "drop": {
            "hosue": "5/2",
            "area": "W-block, DLF Phase 3",
            "city": "Gurgaon",
            "State": "Haryana",
            "pincode": "122002"
          }
        }
      Response:
        {
          request_id: "A3DRE13",
          "request": {
            "customer_name": "Ramesh Yadav",
            "items": [
              {
                "name": "cylinder",
                "type": "volatile"
              },
              {
                "name": "ac",
                "type": "non-volatile"
              }
            ],
            "pickup_address": {
              "house": "123",
              "area": "A-block, Rajender place",
              "city": "Delhi",
              "State": "Delhi",
              "pincode": "110011"
            },
            "drop_address": {
              "hosue": "5/2",
              "area": "W-block, DLF Phase 3",
              "city": "Gurgaon",
              "State": "Haryana",
              "pincode": "122002"
            }
          },
          "response": {
            "estimated_pickup_time": "10",
            "estimated_delivery_time": "60"
          }
        }


----------


**Sample api request and response for 3rd party number 2**
  (It has different api for placing order and fetching status)

  For placing order on 3rd party

    POST /request_pickup
       Request:
          {
            "items": [
              {
                "name": "cylinder",
                "type": "volatile"
              },
              {
                "name": "ac",
                "type": "non-volatile"
              }
            ],
            "pickup_address": "123, A-Block, Rajender Place, Delhi - 110011",
            "drop_address": "5/2, W-block, DLF Phase 3, Gurgaon - 122002"
          }
       Response:
          {
            "id": "883631"
          }

  For fetching status of placed order


    GET /status
       Request:
          {
            "id": "883631"
          }
       Response:
          {
            "eda": "600",
            "edt": "3600",
            "cost": "100"
          }
