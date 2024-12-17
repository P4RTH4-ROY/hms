# Documentation: Hospital Management System (HMS) using MERN Stack

## **Project Overview**
This document outlines the step-by-step process of building a Hospital Management System (HMS) using the MERN stack (MongoDB, Express.js, React.js, Node.js). It includes all the components, directories, and functionalities added during development. The project is structured to be scalable and maintainable.

---

## **Directory Structure**
Here is the directory structure for the project:

```
HMS (Root Directory)
├── server/ (Backend Code)
│   ├── models/
│   │   ├── Appointment.js
│   │   ├── Doctor.js
│   │   └── Patient.js
│   ├── routes/
│   │   ├── appointments.js
│   │   ├── doctors.js
│   │   └── patients.js
│   ├── server.js
│   └── package.json
├── client/ (Frontend Code)
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AppointmentForm.jsx
│   │   │   ├── Appointments.jsx
│   │   │   ├── DoctorForm.jsx
│   │   │   ├── Doctors.jsx
│   │   │   ├── PatientForm.jsx
│   │   │   └── Patients.jsx
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── vite.config.js
│   └── package.json
└── README.md
```

---

## **1. Backend Development**

### **Step 1: Initialize the Backend**
- Navigate to the `server` directory and initialize a Node.js project:
  ```bash
  npm init -y
  ```
- Install the necessary dependencies:
  ```bash
  npm install express mongoose body-parser cors
  ```
- Create the `server.js` file in the `server` directory and configure the server to:
  - Connect to MongoDB.
  - Use Express.js for API routing.
  - Enable CORS for communication with the frontend.

**Code for `server.js`:**
```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const app = express();

const patientsRouter = require('./routes/patients');
const doctorsRouter = require('./routes/doctors');
const appointmentsRouter = require('./routes/appointments');

app.use(express.json());
app.use(cors());
app.use('/patients', patientsRouter);
app.use('/doctors', doctorsRouter);
app.use('/appointments', appointmentsRouter);

mongoose.connect('mongodb+srv://<user>:<password>@cluster.mongodb.net/mern', {})
    .then(() => console.log('MongoDB connected'))
    .catch(err => console.error('MongoDB connection error:', err));

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

### **Step 2: Models**
Create the following models in the `models/` directory:

#### **Appointment.js**
```javascript
const mongoose = require('mongoose');
const appointmentSchema = new mongoose.Schema({
    patientName: String,
    doctorName: String,
    date: Date,
});
module.exports = mongoose.model('Appointment', appointmentSchema);
```

#### **Doctor.js**
```javascript
const mongoose = require('mongoose');
const doctorSchema = new mongoose.Schema({
    name: String,
    specialty: String,
});
module.exports = mongoose.model('Doctor', doctorSchema);
```

#### **Patient.js**
```javascript
const mongoose = require('mongoose');
const patientSchema = new mongoose.Schema({
    name: String,
    age: Number,
    gender: String,
});
module.exports = mongoose.model('Patient', patientSchema);
```

### **Step 3: Routes**
Create the following route files in the `routes/` directory:

#### **appointments.js**
Handles CRUD operations for appointments.

#### **doctors.js**
Handles CRUD operations for doctors.

#### **patients.js**
Handles CRUD operations for patients.

---

## **2. Frontend Development**

### **Step 1: Setup React with Vite**
- Navigate to the `client` directory and create a new React app using Vite:
  ```bash
  npm create vite@latest client -- --template react
  ```
- Install dependencies:
  ```bash
  npm install axios react-router-dom
  ```
- Run the development server:
  ```bash
  npm run dev
  ```

### **Step 2: Components**

#### **Appointments**
- **Files:** `Appointments.jsx`, `AppointmentForm.jsx`
- Features:
  - Add new appointments.
  - Edit existing appointments.
  - Delete appointments.
  - Show success messages on successful operations.

#### **Doctors**
- **Files:** `Doctors.jsx`, `DoctorForm.jsx`
- Features:
  - Add new doctors.
  - Edit existing doctors.
  - Delete doctors.
  - Show success messages on successful operations.

#### **Patients**
- **Files:** `Patients.jsx`, `PatientForm.jsx`
- Features:
  - Add new patients.
  - Edit existing patients.
  - Delete patients.
  - Show success messages on successful operations.

---

## **Key Features Implemented**
1. **CRUD Operations:**
   - Appointments, doctors, and patients can be created, updated, and deleted.
2. **Dynamic Forms:**
   - Forms support both adding and editing functionality.
3. **Success Messages:**
   - User feedback for successful operations.
4. **Frontend-Backend Communication:**
   - API calls using Axios to interact with the backend.
5. **Styling:**
   - (Optional) Add CSS or a library like Tailwind for better UI.

---

## **Next Steps**
1. **Add Search and Filter Functionality:**
   - Allow users to search for appointments, doctors, or patients.
2. **Enhance UI:**
   - Use libraries like Bootstrap or Material-UI for a polished design.
3. **Deploy the Application:**
   - Deploy the backend on platforms like Render or Heroku.
   - Deploy the frontend on Netlify or Vercel.

---

Let me know if there’s anything else to include in the documentation!

