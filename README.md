# JavaScript

JavaScript basics to write tests in Postman

https://developer.mozilla.org/en-US/docs/Web/JavaScript
https://www.w3schools.com/jsref/jsref_number_nan.asp
/*     */ comment

# Console

- console.clear() to delete info from console;
- console.log('Text or Variable') to print info into a console;
- case sensitive
  
# Comments
// and goes comment

# Vaiables

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
5) Arrays view some object property:
   const person1 = {
      firstName: 'Ola',
      lastNAme: 'Olala',
      socialProfiles: [{name: 'Facebook', handle: 'olgA'}, {name: 'Tiktok', handle: 'Olga'}, {name:'Instagram', handle: 'oLga'}]
   
   };
     console.log(person1.socialProfiles[1].name)  ... Tiktok
    

# JSON 

1) object to JSON:
   let json = JSON.stringify(person);
2) JSON to JavaScript Object:
   let newPerson = JSON.parse(json);

# Tests in Postman

1) m.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

2) check response details:
pm.test('Status is UP', function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.status).to.eql("UP");
});











     




