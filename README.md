# JavaScript + Postman

JavaScript basics to write tests in Postman:

https://developer.mozilla.org/en-US/docs/Web/JavaScript

https://www.w3schools.com/jsref/jsref_number_nan.asp

# Comments

/*     */ comment
// and goes comment

# Console

- console.clear() to delete info from console;
- console.log('Text or Variable') to print info into a console;
- case sensitive
  
# Comparison and logical operators in Java script:

https://www.w3schools.com/js/js_comparisons.asp
=== compare value and value type '20' === 20 , 20 === 20


# Variables

- case sensitive
- CamleCase or SnakeCase
- to retrieve type of variable console.log(typeof resp);  returns resp is 'object'

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

   - pm.collectionVariables.set('name', value);
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

6) Getting collection variables in script
  -  pm.collectionVariables.get('productId')
  -  use in test:
     pm.test('Correct product were retrieved', () => {
    const requestedProductId = pm.collectionVariables.get('productId')
    pm.expect(resp.id).equal(requestedProductId);
});

7) Delete collection variables in script:
   - pm.collectionVariables.unset('productId') // delete one variable in parentheses;
   - pm.collectionVariables.clear() // will delete ALL environmental variables;

# Environments in Postman

- one can not change an environment from the script;
- environmental variables overwrite collection variables (have a priority)
- with if clause one can include/exclude tests execution for different environments if (pm.environment.name === 'Testing') {}
- to set environmental variables: pm.environment.set("var_name", value)
- to get environmental variables: pm.environment.get("var_name")
- to delete an environmental variable: pm.environment.unset("var_name")
- to delete ALL environmental variables pm.environment.clear()

# Getting variables in script according to the current scope (collection, environment)
- pm.variables.get('var_name')

# Global variables
- global variables  are accessible throughout the workspace and have the broadest scope in Postman.
  They can be used anywhere among multiple requests and collections within the workspace.
- pm.globals.get(“variable_key”)
- pm.globals.set(“variable_key”, “variable_value”);
- pm.globals.unset(“variable_key”)

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

5) function for Array with forEach and if clause:

function findSeniorEmployees(employees, currentYear) {
    
    let seniorEmployees = [];
    
    employees.forEach((employee) => {
        if(currentYear - employee.yearOfEmployment >= 10 && employee.isActive === true ){
            seniorEmployees.push(employee);
        }
    }
    );
    
	return seniorEmployees;
}

# Object in JavaScript

1) create object:
  const person = {
      firstName: 'Ola',
      lastNAme: 'Olala',
      age: 23
      sayHello: functon () {return 'Hello, my name is  ' + this.firstName;}
   };
3) to view object console.log(person), view some object property : console.log(person.age);
4) if property name(key) has a special characters,  it can be reached in following way: console.log(person.age["social-media"]);
5) in Java script you can add a property to a constant object
6) to iterate through the JavaScript object, when there is a not constant property/key value(it can be changed - MockResponseBody-Check Nested Value):
    for (let key in response){
        console.log(key, response[key]);
    };
   let boardsStatus;
    for (let key in resp.limits){
        console.log(key, resp.limits[key]);
        if(resp.limits[key].hasOwnProperty('boards')){
            boardsStatus = resp.limits[key].boards.totalPerMember.status;
        };
    };
   
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

- find function in Array:
  const personMary = persons.find((person) => person.name === "Mary");
  console.log (personMary.email);
  const persons = [
{
    name:'Jake',
    email: 'jake.p@example.com'
},

{
    name:'Mary',
    email: 'mary.p@example.com'
},

{
    name:'Vova',
    email: 'vova.p@example.com'
}
];

 - transforming an Array with map() function:
   const array2 = array1.map(x => x*2);
   const newArray = person.map( person => person.email) hier wir receiving new array of emails wich are generated from person object of first array with map();

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

# Pre-Request script

- random value between min and max (math.random [0:1)) 
function getRandomNumber (minValue, maxValue) {
    return Math.floor(Math.random()* (maxValue - minValue) + minValue);
}
pm.collectionVariables.set('randomProductQuantity', getRandomNumber(1, 12));


# Chai Assertion Library
	https://www.chaijs.com/api/bdd/
 	https://www.youtube.com/watch?v=NEO8RqnfYec

 - to compare 2 diff objects we use eql assertion, because of equal will compare if both are the same object, but they are different (equal ===)
 - pm.expect().to.be.not.eql()
 - pm.expect().to.be.true;
 - pm.expect().to.be.null;
 - pm.expect().to.be.undefined;
 - pm.expect([]).to.be.empty;
 - pm.expect(2).to.be.oneOf([1,2,3]);
 - pm.expect(2).to.be.within(1, 10);
 - pm.expect([1,2,3]).to.include(2);
 - pm.expect([1,2,3]).to.have.lengthOf(3);
 - pm.expect('Some song').to.match(/^Some/); regular expressions
 - instanceof, .property, .string, .keys, .ordered, .any, .all
 - pm.expect(resp).to.be.an('array')
 - pm.expect(resp).to.be.an('object')

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

6) When 'const resp' is defined as global variable and by running a request there is no query variable we receive an error and all tests are not done, because there is no json in response. To receive status code test executed, we can declare resp as global variable and initialize it in test. In this case all other test will receive the variable 'resp' and use it, and all set env/collection variables commands, that use resp should be inside tests.
  
const resp;

pm.test("Created order is in the list", () => {
    resp = pm.response.json();
    let lastOrderId = pm.collectionVariables.get("lastOrderId");
    let isOrderIdInResponse = false;
    for (let i = 0; i < resp.length; i++){
        if (resp[i].id === lastOrderId){
        isOrderIdInResponse = true}
    }
    pm.expect(isOrderIdInResponse).to.be.true;
})

# Test headers
- to access headers from response: pm.response.headers.get('nameOfProperty')
- assertion for the header properties:
  pm.test("Is header Date exists", () => {
    pm.response.to.have.header('Date');
    pm.expect(pm.response.headers.get('Date')).to.contain('07 Dec 2023');
});

# Test cookies
- to access cookies from response: pm.cookies.get('sessionId')
- assertion for the cookie properties:
  pm.expect(pm.cookies.has('sessionId')).to.be.true;
  pm.expect(pm.cookies.get('sessionId')).to.eql('ad3se3ss8sg7sg3');

# Test Workflows
- to set an execution order it is needed to add in Tests the script:   pm.setNextRequest("Request_Name"), Request ID can be used instead the Request name (pm.info.requestName, pm.info.requestID)
- the order , in which pm.setNextRequest("Request_Name") script is placed is not important, it is executed at the end
- to stop a workflow execution:  pm.setNextRequest(null) otherwise it can lead to infinity loop
- to set one test execution max X times, it is possible to set a variable, which contains a number of request runs and check it with If-clause
  

# Run Tests On Continuous Integration Server
1) Postman CLI
- install Postman CLI in Windows PowerShell: https://learning.postman.com/docs/postman-cli/postman-cli-installation/#windows-installation
- in Postman select Automate runs via CLI
- generate API Key for the collection
- in collection variables to persist all current to initial value
- run collection in console : postman login [key], postman collection run [collectionId]
- postman logout
- run collection without login is possible with postman collection run [viaAPI link]
- running from file: export collection to json file and in console: postman collection run + path to file
- to run a collection with a specific environment, one need to add an environmental ID (under Environments -> Info): postman collection run [collectionId ]-e [environmental ID]
- other CLI options https://learning.postman.com/docs/postman-cli/postman-cli-options/   :
  -> --bail  stop execution when a test fаils
  -> --env-var [env_var_name] = [env_var_value]  specifies environment variables via the command line
  ->  -i [folderID] or [requestID] runs only the specified folder/s  or request/s  from the collection using folder Id or Name (id is preferred)
  ->  --ignore-redirects prevents the Postman CLI from automatically following 3XX redirect responses
  ->  --insecure  disabled certificat validation SSL checks
  ->  -- verbose provides more details about execution of request for debugging purposes
  
2) Newman
  - install Node js https://nodejs.org/en/download
  - install Newman https://github.com/postmanlabs/newman#installation
  - in collection ... share -> viaAPI -> generate key (manage account-> API keys) -> copy link
  - in collection variables to persist all current to initial value
  - in console  newman run [link] or newman run [path to file], when a file contains special characters the entire file name should be put in ' '
  - to run a collection with a specific environment neman run [link] -e [environment link], -e https://api.postman.com/environments/[environmentID]?apikey=[key]
  - Neman command line options  https://github.com/postmanlabs/newman#command-line-options

- HTML report in Newman
    -> to install https://www.npmjs.com/package/newman-reporter-htmlextra
    -> newman run  [link] -e [environment link] -r htmlextra
    -> report will be in a folder newman in the current directory, in console thereis no report more
    -> to have report in both places -r cli,htmlextra or -r 'cli,htmlextra'
    -> to have env. variables in report --reporter-htmlextra-showEnvironmentData

- JUnit XML report in Newman: newman run  [link] -e [environment link] -r cli,junit
  https://github.com/postmanlabs/newman?tab=readme-ov-file#junitxml-reporter

- other Newman config options: --bail, --env--var, --folder, --verbose -> https://www.npmjs.com/search?ranking=popularity&q=newman-reporter-

# Postman Tests run with Jenkins

- install Docker Desktop https://www.docker.com/products/docker-desktop/
- in cmd to run Jenkins in a container: docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -v jenkins_home:/var/jenkins_home --env JAVA_OPTS="-Dfile.encoding=UTF8" vdespa/jenkins-postman (to stop Jenkins ctrl+c)
- there is a pass in log, localhost 8080
- 
- create a Job with freestyle project:
  in build check postmanCLI/newman installation and run as usually.
  It is a good practice to hide a keys with Dashbord -> Manage Jenkins -> Manage Credentials -> Global Credentials -> add -> Secret Text -> key and ID name for key.
  In Job configure build environment with use secret text, give variable name and with $ add to run command $POSTMAN_API_KEY
  
- create Job with Jenkinsfile(pipeline):
  to configure Pipeline, go to Postman -> run on ci/cd -> check collection name, environment, ci/cd provider, operating system for CI/CD, copy code and
  add an environment variable, delete unnecessary installations
  to configure Pipeline with newman, one can use the same template as for postman CLI

  to receive a HTTP report with Jenkinsfile one should add:
  -  to the file command --reporters cli,htmlextra --reporter-htmlextra-export newman/report.html 
  -  Manage Jenkins -> Plugins -> install HTML plugin and Script Console 
  -    post {
        always {
            publishHTML target: [
                reportName: 'Newman',
                reportDir: 'newman',
                reportFiles: 'report.html',
                reportTitles: 'Postman API tests',
                keepAll: true,
                alwaysLinkToLastBuild: true,
                allowMissing: false
            ]
        }
    }

 - freestyle project: to receive a XML report:
	  -  to the file command --reporters cli,junit --reporter-junit-export newman/report.xml
	  -  to the post actions junit 'newman/report.xml'


     




