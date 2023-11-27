# JavaScript + Postman

JavaScript basics to write tests in Postman

https://developer.mozilla.org/en-US/docs/Web/JavaScript
https://www.w3schools.com/jsref/jsref_number_nan.asp
/*     */ comment

# Console

- console.clear() to delete info from console;
- console.log('Text or Variable') to print info into a console;
- case sensitive
  
# Comments
=== compare value and value type '20' === 20 , 20 === 20
// and goes comment

# Variables

- case sensitive
- CamleCase or SnakeCase

1) ways to declare a variable:

- var  firstName = 'Ira';
- let lastName = "Han";
- let age = 20;
- let email;
- let isMarried = true;
- let fullName;
- console.log(firstName, age, email);

2) change content of a variable
   
   - firstName = 'Olga';
   - email = 'olga12@regl.com'
     
3) Constant variable - protect from overriding
   - const webUrl = 'http:....'

4) there are GLOBAL and BLOCK scope variables:
   - global variable can be used in a block
   - global and block variables can have te same name
   - inside a block a value of a global variable can be changed but you can not use a block variable in a global scope
  
5) Setting Postman variables from scripts:

   - pm.collectionVariables.set('key', value);
   - to set a collections property we have to be sure, that it has an expected value:
     
   pm.test('At list one product ID exists', () => {
      const resp = pm.response.json();
      pm.expect(resp).to.be.an('array');
      pm.expect(resp.length).to.be.above(0);

      const product = resp[0];

      pm.expect(product).to.be.an('object');
      pm.expect(product).to.haveOwnProperty('id');
      pm.expect(product.id).to.be.a('number');
      pm.expect(product).haveOwnProperty('inStock');
      pm.expect(product.inStock).is.true;
      pm.collectionVariables.set('productId', resp[2].id);

})

# Getting variables in script
  -  pm.collectionVariables.get('productId')
  -  use in test:
     pm.test('Correct product were retrieved', () => {
    const requestedProductId = pm.collectionVariables.get('productId')
    pm.expect(resp.id).equal(requestedProductId);
});

# Text template and concatination

   - fullName = firstName + lastName;
   - fullName = `${firstName} ${lastName}`
   - let fullName = `${firstName} ${lastName}`;
   - let info = `My name is ${firstName} and sirname is ${lastName}`; console.log(info);
   - let infoAge = ` I am ${2023-1990} years old`;
   - let outlet = '2'; let number = parseInt('2');
  
# Swap two variables in JavaScript

- destructuring assignment
  [firstName, lastName] = [lastName, firstName];
- with temporary variable
- another 2 ways https://dmitripavlutin.com/swap-variables-javascript/

# Functions

1) functions definition:
        function add(a, b) {
          let sum = a + b;
          return sum
        }
2) arrow functions:
   const add = (a, b) => a + b;
   
3) build-in functions https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor
   
4) callback functions:
   https://developer.mozilla.org/en-US/docs/Web/API/setTimeout

# Object in JavaScript

1) create object:
  const person = {
      firstName: 'Ola',
      lastNAme: 'Olala',
      age: 23
      sayHello: functon () {return 'Hello, my name is  ' + this.firstName;}
   };
3) to view object console.log(person), view some object property : console.log(person.age)
4) in Java script you can add a property to a constant object
   
# Arrays []

- for loop for Array:
  let number = [1,3,5,7,9]
  for (let i = 0; i<number.length; i++){
     console.log(number[i]);
  }

- forEach:
  pm.test("Created order is in the list", () => {
    let lastOrderId = pm.collectionVariables.get("lastOrderId");
    let isOrderIdInResponse = false;
    resp.forEach((order) => {
        if (order.id === lastOrderId){
        isOrderIdInResponse = true}
    });
    pm.expect(isOrderIdInResponse).to.be.true;
})
  
- methods: push (add to the end value and returns length), length (arrays size), pop (delete last und returns its value), shift (delete first und returns value), etc
  
- view some object property from Array:
   - console.log(person1.socialProfiles[1].name)
   const person1 = {
      firstName: 'Ola',
      lastNAme: 'Olala',
      socialProfiles: [{name: 'Facebook', handle: 'olgA'}, {name: 'Tiktok', handle: 'Olga'}, {name:'Instagram', handle: 'oLga'}]
   
   };
   !!!... Tiktok
    
# JSON 

1) object to JSON:
   let json = JSON.stringify(person);
2) JSON to JavaScript Object:
   let newPerson = JSON.parse(json);
3) Navigate through JSON
   - const firstPostalCode = response[0].Item01.Data[0].Results[0].Contact.Address.PostalCode;
[
    {
        "Item01": {
            "MetaInfo": {
                "Timestamp": "2023-02-16T08:15:21.000+0000"
            },
            "Data": [
                {
                    "_type": "SearchResultsContact",
                    "DataId": 1987,
                    "Results": [
                        {
                            "Relevance": 0.5,
                            "Contact": {
                                "Name": "John Doe",
                                "Phone": "+1-555-123-4567",
                                "Email": "johndoe@email.com",
                                "Address": {
                                    "Street": "123 Main St",
                                    "City": "Anytown",
                                    "State": "CA",
                                    "PostalCode": "12345"
                                },
                                "Active": true,
                                "Notes": "New customer"
                            }
                        }
                    ]
                }
            ]
        }
    }
]

   

# Tests in Postman

1) m.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

2) check response details:
pm.test('Status is UP', function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.status).to.eql("UP");
});

3) pm.test("Check product is in stock", () => {
    const resp = pm.response.json();
    pm.expect(resp.inStock).to.be.true;
})

4) pm.test("Check price", () => {
    const resp = pm.response.json();
    pm.expect(resp.price).to.be.a('number');
    pm.expect(resp.price).to.be.above(0);
})

5) const resp = pm.response.json();
pm.test("Error message", () => {
    pm.expect(resp.error).to.have.string("Invalid value");
    pm.expect(resp.error).to.contain("Invalid value");
})

6) const resp = pm.response.json();

pm.test("Created order is in the list", () => {
    let lastOrderId = pm.collectionVariables.get("lastOrderId");
    let isOrderIdInResponse = false;
    for (let i = 0; i < resp.length; i++){
        if (resp[i].id === lastOrderId){
        isOrderIdInResponse = true}
    }
    pm.expect(isOrderIdInResponse).to.be.true;
})







     




