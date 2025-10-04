# Postman API Testing

**Author:** Sozibul Islam  
**Date:** 2025-10-04   

---

## 📄 Project Overview

This project demonstrates **API testing** using **Postman** with automated test scripts written in JavaScript.

### ✅ Key Features

- Validate status codes
- Verify response time and headers
- Check JSON structure and values
- Handle positive and negative test cases
- Use environment and global variables for data reuse

---

## 🧪 Test Script Examples

```javascript
// ✅ Status Code Check
pm.test("Status code is 200", () => 
    pm.response.to.have.status(200)
);

// ✅ Header Check
pm.test("Content-Type is JSON", () => 
    pm.expect(pm.response.headers.get("Content-Type")).to.match(/application\/json/)
);

// ✅ Body Keys Check
pm.test("Response has ID and name", () => 
    pm.expect(pm.response.json()).to.include.keys("id", "name")
);

// ✅ Type Validation
pm.test("Check booking id type number", () => {
    const jsonData = pm.response.json();
    pm.expect(jsonData.bookingid).to.be.a('number');
});



// Set environment variable
const jsonData = pm.response.json();
pm.environment.set("bookingId", jsonData.bookingid);

// Get environment variable
console.log(pm.environment.get("bookingId"));


// Set global variable manually
pm.globals.set("additionalneeds", "Baggage");

// Set global variable from response
const jsonData = pm.response.json();
pm.globals.set("Baggage", jsonData.booking.additionalneeds);

// Get global variable
console.log(pm.globals.get("Baggage"));

// Delete global variable
pm.globals.unset("Baggage");


// Successful POST (200 or 202)
pm.test("Successful POST request", () => 
    pm.expect(pm.response.code).to.be.oneOf([200, 202])
);

