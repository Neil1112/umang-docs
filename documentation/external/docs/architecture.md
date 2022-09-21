# Tech Stack & Code Architecture/Organisation

---

This document gives the description of the technologies involved, and the project architecture. 

## Technologies

The Project is structured in a _Monolith_ structure. Thus the production (i.e - the master branch) has:
- Single server
- Single remote database

### The Stack

The tech-stack chosen for the project is the MERN stack. MERN stands for a group of four technologies used in synergy.
- M stands for MongoDB - A NoSQL Database
- E stands for ExpressJS - A minimalist web framework for NodeJS
- R stands for ReactJS - A frontend library
- N stands for NodeJS - A Javascript Runtime Environment

### Database details

MongoDB is chosen as the database for the project. It is a NoSQL database. Its cloud solutioln named MongoDB Atlas is integrated in the project. The details for the current configuration is as follows:
- Database Type - Cloud
- Service Name - MongoDB Atlas
- Cluster Type - Shared
- Cloud Provider - Google
- Region - Mumbai (asia-south-1)
- Cluster Tier - M0 Sandbox
- Cluster Tier Pricing - FREE
- Connection String - mongodb+srv://admin:_ENTER_PASSWORD_%21@cluster0.x2jgv.gcp.mongodb.net/admin


