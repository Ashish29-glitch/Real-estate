# 🏠 Full-Stack Real Estate Marketplace

A modern, feature-rich real estate marketplace application built with React, Express.js, and MongoDB. This platform allows users to browse properties, book visits, manage favorites, and property owners to list their properties with an intuitive multi-step form wizard.

![Real Estate Marketplace](https://img.shields.io/badge/Real%20Estate-Marketplace-blue?style=for-the-badge&logo=home)
![React](https://img.shields.io/badge/React-18.2.0-61DAFB?style=flat-square&logo=react)
![Express.js](https://img.shields.io/badge/Express.js-4.18.2-000000?style=flat-square&logo=express)
![MongoDB](https://img.shields.io/badge/MongoDB-4.16.2-47A248?style=flat-square&logo=mongodb)
![Auth0](https://img.shields.io/badge/Auth0-Authentication-EB5424?style=flat-square&logo=auth0)

## 📋 Table of Contents

- [🏠 Full-Stack Real Estate Marketplace](#-full-stack-real-estate-marketplace)
  - [📋 Table of Contents](#-table-of-contents)
  - [✨ Features](#-features)
  - [🎯 Goals](#-goals)
  - [🛠️ Technologies Used](#️-technologies-used)
  - [🏗️ Architecture](#️-architecture)
  - [📁 Project Structure](#-project-structure)
  - [🚀 Getting Started](#-getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
    - [Environment Setup](#environment-setup)
    - [Running the Application](#running-the-application)
  - [📖 Usage](#-usage)
  - [🔌 API Documentation](#-api-documentation)
  - [🎨 UI Components](#-ui-components)
  - [🔒 Authentication](#-authentication)
  - [🗄️ Database Schema](#️-database-schema)
  - [🚀 Deployment](#-deployment)
  - [🤝 Contributing](#-contributing)
  - [📄 License](#-license)
  - [👥 Authors](#-authors)
  - [🙏 Acknowledgments](#-acknowledgments)

## ✨ Features

### 🏡 Core Property Features

- **Property Browsing**: Browse all available properties with detailed information
- **Advanced Search**: Filter properties by title, city, or country
- **Interactive Maps**: View properties on interactive Leaflet maps with geocoding
- **Property Details**: Comprehensive property information including facilities, pricing, and location
- **Image Gallery**: High-quality property images hosted on Cloudinary

### 👤 User Management

- **Secure Authentication**: OAuth2 integration with Auth0
- **User Profiles**: Automatic user registration and profile management
- **Favorites System**: Save and manage favorite properties
- **Booking System**: Schedule property visits with date selection
- **Booking Management**: View and cancel scheduled visits

### 🏢 Property Management

- **Add Properties**: Multi-step form wizard for property listing
- **Location Selection**: Interactive map-based location selection
- **Image Upload**: Secure image upload via Cloudinary widget
- **Facility Management**: Detailed facility information (bedrooms, bathrooms, parking)
- **Ownership Tracking**: Property ownership and management

### 🎨 User Experience

- **Responsive Design**: Mobile-first responsive design
- **Modern UI**: Premium UI components with Mantine design system
- **Smooth Animations**: Framer Motion animations for enhanced UX
- **Toast Notifications**: Real-time feedback for user actions
- **Loading States**: Proper loading indicators and error handling

## 🎯 Goals

This project aims to provide a comprehensive real estate marketplace that:

- **Connects Property Owners and Buyers**: Seamless platform for property listing and discovery
- **Provides Rich User Experience**: Modern, intuitive interface with powerful features
- **Ensures Security**: Robust authentication and data protection
- **Offers Scalability**: Well-architected backend ready for growth
- **Delivers Performance**: Optimized frontend with efficient data fetching
- **Maintains Code Quality**: Clean, maintainable codebase following best practices

## 🛠️ Technologies Used

### Frontend (Client)

- **React 18.2.0** - Modern UI library with hooks and concurrent features
- **Vite 4.2.0** - Fast build tool and development server
- **React Router 6.10.0** - Declarative routing for React
- **React Query 3.39.3** - Powerful data synchronization for React
- **Auth0 React SDK** - Authentication and user management
- **Mantine 6.0.16** - Modern React components library
- **Leaflet & React-Leaflet** - Interactive maps and geocoding
- **Framer Motion** - Production-ready motion library
- **Axios** - Promise-based HTTP client
- **Swiper** - Modern mobile touch slider
- **React Toastify** - Toast notifications
- **Day.js** - Lightweight date manipulation library

### Backend (Server)

- **Express.js 4.18.2** - Fast, unopinionated web framework
- **Prisma 4.16.2** - Next-generation ORM for TypeScript & Node.js
- **MongoDB** - NoSQL document database
- **Auth0 JWT Bearer** - JWT token validation middleware
- **CORS** - Cross-origin resource sharing
- **Cookie Parser** - Parse HTTP request cookies
- **Dotenv** - Environment variable management
- **Nodemon** - Auto-restart during development

### External Services

- **Auth0** - Authentication and authorization
- **Cloudinary** - Image hosting and optimization
- **OpenStreetMap** - Map tiles and data
- **ESRI Geocoder** - Address geocoding service
- **Vercel** - Deployment platform

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    CLIENT (React + Vite)                         │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ App → Layout (Auth initialization)                      │    │
│  │ ├── Layout Effect: getAccessToken() → createUser()     │    │
│  │ └── Outlet (page component)                            │    │
│  └────────────────────────────────────────────────────────┘    │
│                         ↓                                        │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Pages: Website, Properties, Property, Bookings, Fav    │    │
│  │ ├── useProperties() → getAllProperties()               │    │
│  │ ├── useBookings() → getAllBookings()                   │    │
│  │ └── useFavourites() → getAllFav()                      │    │
│  └────────────────────────────────────────────────────────┘    │
│                         ↓                                        │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Components with Context (UserDetailContext)            │    │
│  │ ├── Heart (toFav mutation)                             │    │
│  │ ├── BookingModal (bookVisit mutation)                  │    │
│  │ ├── AddPropertyModal (createResidency mutation)        │    │
│  │ └── ProfileMenu                                        │    │
│  └────────────────────────────────────────────────────────┘    │
│                         ↓                                        │
│         axios instance → BASE_URL/api                          │
│                         ↓                                        │
└─────────────────────────────────────────────────────────────────┘
                          ↓ HTTP
┌─────────────────────────────────────────────────────────────────┐
│               SERVER (Express.js + Prisma)                       │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Routes:                                                 │    │
│  │ ├── /api/user (createUser, bookVisit, toFav, etc)    │    │
│  │ └── /api/residency (create, allresd, :id)            │    │
│  └────────────────────────────────────────────────────────┘    │
│                         ↓                                        │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Middleware:                                             │    │
│  │ ├── jwtCheck (Auth0 JWT validation)                   │    │
│  │ ├── express.json() (body parsing)                     │    │
│  │ └── cors()                                             │    │
│  └────────────────────────────────────────────────────────┘    │
│                         ↓                                        │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Controllers:                                            │    │
│  │ ├── userCntrl: CRUD user bookings/favorites           │    │
│  │ └── resdCntrl: CRUD property listings                 │    │
│  └────────────────────────────────────────────────────────┘    │
│                         ↓                                        │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Prisma ORM ↔ MongoDB                                   │    │
│  │ Models: User, Residency                                │    │
│  └────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

## 📁 Project Structure

```
Full-stack-real-estate-youtube-main/
├── client/                          # Frontend React Application
│   ├── public/                      # Static assets
│   ├── src/
│   │   ├── components/              # Reusable UI components
│   │   │   ├── AddLocation/         # Location selection component
│   │   │   ├── AddPropertyModal/    # Multi-step property form
│   │   │   ├── BasicDetails/        # Property details form
│   │   │   ├── BookingModal/        # Booking date picker
│   │   │   ├── Companies/           # Partner logos
│   │   │   ├── Contact/             # Contact information
│   │   │   ├── Facilities/          # Property facilities form
│   │   │   ├── Footer/              # Site footer
│   │   │   ├── GeoCoderMarker/      # Map geocoding component
│   │   │   ├── GetStarted/          # Call-to-action section
│   │   │   ├── Header/              # Navigation header
│   │   │   ├── Heart/               # Favorite toggle button
│   │   │   ├── Hero/                # Hero banner section
│   │   │   ├── Layout/              # Main layout wrapper
│   │   │   ├── Map/                 # Interactive map display
│   │   │   ├── ProfileMenu/         # User dropdown menu
│   │   │   ├── PropertyCard/        # Property card component
│   │   │   ├── Residencies/         # Properties carousel
│   │   │   ├── SearchBar/           # Property search/filter
│   │   │   ├── UploadImage/         # Image upload component
│   │   │   └── Value/               # Value proposition section
│   │   ├── context/                 # React context providers
│   │   │   └── UserDetailContext.js # User state management
│   │   ├── hooks/                   # Custom React hooks
│   │   │   ├── useAuthCheck.jsx     # Authentication validation
│   │   │   ├── useBookings.jsx      # Bookings data fetching
│   │   │   ├── useCountries.jsx     # Country data formatting
│   │   │   ├── useFavourites.jsx    # Favorites data fetching
│   │   │   ├── useHeaderColor.jsx   # Header scroll effects
│   │   │   └── useProperties.jsx    # Properties data fetching
│   │   ├── pages/                   # Page-level components
│   │   │   ├── Website.jsx          # Landing page
│   │   │   ├── Bookings/            # User bookings page
│   │   │   │   └── Bookings.jsx
│   │   │   ├── Favourites/          # User favorites page
│   │   │   │   └── Favourites.jsx
│   │   │   ├── Properties/          # Properties listing page
│   │   │   │   └── Properties.jsx
│   │   │   └── Property/            # Property detail page
│   │   │       └── Property.jsx
│   │   ├── utils/                   # Utility functions
│   │   │   ├── accordion.jsx        # Accordion utilities
│   │   │   ├── api.js               # API client functions
│   │   │   ├── common.js            # Common helper functions
│   │   │   └── slider.json          # Carousel configuration
│   │   ├── App.css                  # Global styles
│   │   ├── App.jsx                  # Main App component
│   │   ├── index.css                # Base styles
│   │   └── main.jsx                 # Application entry point
│   ├── index.html                   # HTML template
│   ├── package.json                 # Frontend dependencies
│   ├── vercel.json                  # Vercel deployment config
│   └── vite.config.js               # Vite configuration
│
└── server/                          # Backend Express Application
    ├── config/                      # Configuration files
    │   ├── auth0Config.js           # Auth0 JWT configuration
    │   └── prismaConfig.js          # Prisma database config
    ├── controllers/                 # Business logic controllers
    │   ├── resdCntrl.js             # Property operations
    │   └── userCntrl.js             # User operations
    ├── data/                        # Seed data
    │   └── Residency.json           # Sample property data
    ├── prisma/                      # Database schema
    │   └── schema.prisma            # Prisma schema definition
    ├── routes/                      # API route definitions
    │   ├── residencyRoute.js        # Property routes
    │   └── userRoute.js             # User routes
    ├── index.js                     # Server entry point
    ├── package.json                 # Backend dependencies
    ├── vercel.json                  # Vercel deployment config
    └── .env.example                 # Environment variables template
```

## 🚀 Getting Started

### Prerequisites

Before running this application, make sure you have the following installed:

- **Node.js** (version 16 or higher)
- **npm** or **yarn** package manager
- **MongoDB** database (local or cloud instance)
- **Git** for version control

### Installation

1. **Clone the repository**

   ```bash
   git clone [https://github.com/Ashish29-glitch/Real-estate.git]
   cd full-stack-real-estate-marketplace
   ```

2. **Install client dependencies**

   ```bash
   cd client
   npm install
   ```

3. **Install server dependencies**
   ```bash
   cd ../server
   npm install
   ```

### Environment Setup

1. **Set up Auth0 Application**
   - Create an Auth0 account and application
   - Configure the following settings:
     - Domain: `dev-03ifqltxbr6nn0hn.us.auth0.com`
     - Client ID: `RXlGXkr49Ev5MHpvAC6vKkZ4bVn11iwl`
     - Allowed Callback URLs: `http://localhost:5173, https://your-domain.com`
     - Allowed Logout URLs: `http://localhost:5173, https://your-domain.com`
     - Allowed Web Origins: `http://localhost:5173, https://your-domain.com`

2. **Set up Cloudinary Account**
   - Create a Cloudinary account
   - Get your cloud name, API key, and API secret

3. **Configure Environment Variables**

   Create a `.env` file in the `server` directory:

   ```env
   PORT=8000
   DATABASE_URL="mongodb+srv://username:password@cluster.mongodb.net/real_estate_db?retryWrites=true&w=majority"
   AUTH0_DOMAIN=dev-03ifqltxbr6nn0hn.us.auth0.com
   AUTH0_AUDIENCE=http://localhost:8000
   CLOUDINARY_CLOUD_NAME=your_cloud_name
   CLOUDINARY_API_KEY=your_api_key
   CLOUDINARY_API_SECRET=your_api_secret
   ```

4. **Database Setup**
   ```bash
   cd server
   npx prisma generate
   npx prisma db push
   ```

### Running the Application

1. **Start the backend server**

   ```bash
   cd server
   npm start
   ```

   The server will run on `http://localhost:8000`

2. **Start the frontend development server**

   ```bash
   cd client
   npm run dev
   ```

   The client will run on `http://localhost:5173`

3. **Access the application**
   - Open your browser and navigate to `http://localhost:5173`
   - Click "Login" to authenticate with Auth0
   - Start browsing properties or add your own listings!

## 📖 Usage

### For Property Seekers

1. **Browse Properties**
   - Visit the homepage to see featured properties
   - Use the search bar to filter by location or property type
   - Click on property cards to view detailed information

2. **Book Property Visits**
   - Click "Book your visit" on any property
   - Select your preferred date from the calendar
   - Confirm your booking

3. **Manage Favorites**
   - Click the heart icon on properties to add to favorites
   - Access your favorites from the profile menu

### For Property Owners

1. **Add New Properties**
   - Click "Add Property" in the navigation
   - Follow the 4-step wizard:
     - **Location**: Select country, city, and address
     - **Images**: Upload property photos via Cloudinary
     - **Details**: Enter title, description, and pricing
     - **Facilities**: Specify bedrooms, bathrooms, and parking

2. **Manage Your Listings**
   - View all your properties in "My Properties"
   - Edit or remove listings as needed

## 🔌 API Documentation

### Base URL

```
http://localhost:8000/api
```

### User Endpoints

| Method | Endpoint                  | Authentication | Description              |
| ------ | ------------------------- | -------------- | ------------------------ |
| POST   | `/user/register`          | JWT Required   | Register/create user     |
| POST   | `/user/bookVisit/:id`     | JWT Required   | Book a property visit    |
| POST   | `/user/allBookings`       | None           | Get user's bookings      |
| POST   | `/user/removeBooking/:id` | JWT Required   | Cancel booking           |
| POST   | `/user/toFav/:rid`        | JWT Required   | Toggle property favorite |
| POST   | `/user/allFav`            | JWT Required   | Get user's favorites     |

### Property Endpoints

| Method | Endpoint             | Authentication | Description                 |
| ------ | -------------------- | -------------- | --------------------------- |
| POST   | `/residency/create`  | JWT Required   | Create new property listing |
| GET    | `/residency/allresd` | None           | Get all properties          |
| GET    | `/residency/:id`     | None           | Get single property details |

### Request/Response Examples

**Book a Visit**

```bash
POST /api/user/bookVisit/64f1a2b3c4d5e6f7g8h9i0j
Authorization: Bearer <jwt_token>
Content-Type: application/json

{
  "email": "user@example.com",
  "date": "15/12/2023"
}
```

**Create Property**

```bash
POST /api/residency/create
Authorization: Bearer <jwt_token>
Content-Type: application/json

{
  "title": "Modern Apartment",
  "description": "Beautiful 2BR apartment in downtown",
  "price": 2500,
  "address": "123 Main St",
  "city": "New York",
  "country": "United States",
  "image": "https://cloudinary.com/image.jpg",
  "facilities": {
    "bedrooms": 2,
    "bathrooms": 1,
    "parkings": 1
  },
  "userEmail": "owner@example.com"
}
```

## 🎨 UI Components

The application features a comprehensive component library:

- **Layout Components**: Header, Footer, Layout wrapper
- **Form Components**: Multi-step forms, date pickers, search bars
- **Data Display**: Property cards, carousels, maps
- **Interactive Elements**: Modals, dropdowns, buttons
- **Feedback Components**: Loading spinners, toast notifications

All components are built with Mantine UI library for consistency and accessibility.

## 🔒 Authentication

The application uses Auth0 for secure authentication:

- **OAuth2 Flow**: Industry-standard authentication
- **JWT Tokens**: Secure API access with bearer tokens
- **User Management**: Automatic user registration
- **Protected Routes**: Server-side route protection
- **Session Management**: Persistent login sessions

## 🗄️ Database Schema

### User Model

```prisma
model User {
  id               String          @id @default(auto())
  name             String?
  email            String          @unique
  image            String?
  bookedVisits     Json[]          // [{id: string, date: string}]
  favResidenciesID String[]        // Array of property IDs
  ownedResidencies Residency[]     // One-to-many relationship
}
```

### Residency Model

```prisma
model Residency {
  id          String          @id @default(auto())
  title       String
  description String
  price       Int
  address     String
  city        String
  country     String
  image       String
  facilities  Json            // {bathrooms: number, bedrooms: number, parkings: number}
  userEmail   String
  owner       User            // Many-to-one relationship
  createdAt   DateTime        @default(now())
  updatedAt   DateTime        @updatedAt

  @@unique(fields: [address, userEmail])  // Unique constraint
}
```

## 🚀 Deployment

### Frontend Deployment (Vercel)

1. **Connect Repository**
   - Import your GitHub repository to Vercel
   - Set build settings:
     - Build Command: `npm run build`
     - Output Directory: `dist`
     - Install Command: `npm install`

2. **Environment Variables**
   - Set Auth0 configuration in Vercel dashboard
   - Configure API base URL for production

### Backend Deployment (Vercel)

1. **Serverless Functions**
   - Vercel automatically detects the Express app
   - Routes are configured via `vercel.json`

2. **Database Connection**
   - Use MongoDB Atlas for production database
   - Update `DATABASE_URL` in environment variables

### Production URLs

- Frontend: `https://your-app.vercel.app`
- Backend API: `https://your-api.vercel.app`

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Development Guidelines

- Follow React and Express.js best practices
- Write clear, concise commit messages
- Test your changes thoroughly
- Update documentation as needed
- Maintain code quality and consistency

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Your Name** - _Initial work_ - [Your GitHub](https://github.com/your-username)

## 🙏 Acknowledgments

- **Auth0** for authentication services
- **Cloudinary** for image hosting
- **Mantine** for UI components
- **Prisma** for database ORM
- **Vercel** for deployment platform
- **OpenStreetMap** for map data
- **ESRI** for geocoding services

---

**Happy coding! 🏠✨**

If you find this project helpful, please give it a ⭐ on GitHub!

