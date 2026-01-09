# Redux CRUD - E-Commerce Shopping Cart Application

A modern React e-commerce application demonstrating Redux Toolkit state management with shopping cart functionality. This project showcases CRUD operations, async actions, and persistent cart data management.

## Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Available Scripts](#available-scripts)
- [State Management](#state-management)
- [Components Overview](#components-overview)
- [API Integration](#api-integration)
- [Contributing](#contributing)
- [License](#license)

## Features

- 🛒 **Shopping Cart Management**: Add, remove, and manage items in your cart
- 🔄 **Real-time Updates**: Cart updates reflect immediately across the application
- 💾 **Data Persistence**: Cart data is automatically saved to and loaded from a backend
- 🔔 **Notification System**: User-friendly notifications for cart operations
- 📦 **Product Catalog**: Browse and add products to your cart
- 🎨 **Modern UI**: Clean and responsive user interface with CSS Modules
- ⚡ **Redux Toolkit**: Efficient state management using Redux Toolkit

## Technologies Used

- **React** (^18.0.0) - UI library
- **Redux Toolkit** (^2.8.2) - State management
- **React Redux** (^9.2.0) - React bindings for Redux
- **React Scripts** (^5.0.1) - Build tooling
- **CSS Modules** - Scoped styling

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (version 14.0.0 or higher)
- **npm** (version 6.0.0 or higher) or **yarn**

You can verify your installations by running:

```bash
node --version
npm --version
```

## Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd redux_CRUD
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

   or if you're using yarn:

   ```bash
   yarn install
   ```

3. **Configure the database URL**

   Open `src/util/cfg.js` and replace `'YOUR_DATABASE_URL'` with your actual database/API endpoint URL.

   ```javascript
   export const DB_LINK = 'https://your-api-endpoint.com/cart.json'
   ```

## Configuration

The application requires a backend API endpoint for cart data persistence. Configure your database URL in:

```
src/util/cfg.js
```

The API should support:
- **GET** request to fetch cart data
- **PUT** request to update cart data

Expected response format:
```json
{
  "items": [
    {
      "id": "p1",
      "name": "Product Name",
      "price": 10,
      "quantity": 2,
      "totalPrice": 20
    }
  ],
  "totalQuantity": 2
}
```

## Usage

1. **Start the development server**

   ```bash
   npm start
   ```

   The application will open in your browser at `http://localhost:3000`

2. **Browse products**

   - View available products in the main shop area
   - Each product displays its title, description, and price

3. **Manage your cart**

   - Click "Add to Cart" on any product to add it to your cart
   - Click the cart button in the header to view your cart
   - Increase or decrease item quantities
   - Remove items from the cart
   - Cart data is automatically saved to the backend

4. **Notifications**

   - The app displays notifications for:
     - Pending operations (sending cart data)
     - Success messages (cart saved successfully)
     - Error messages (failed operations)

## Project Structure

```
redux_CRUD/
├── public/                 # Static assets
│   ├── index.html
│   └── ...
├── src/
│   ├── components/         # React components
│   │   ├── Cart/          # Cart-related components
│   │   │   ├── Cart.js
│   │   │   ├── CartItem.js
│   │   │   └── CartButton.js
│   │   ├── Layout/        # Layout components
│   │   │   ├── Layout.js
│   │   │   └── MainHeader.js
│   │   ├── Shop/          # Product components
│   │   │   ├── Products.js
│   │   │   └── ProductItem.js
│   │   └── UI/            # Reusable UI components
│   │       ├── Card.js
│   │       └── Notification.js
│   ├── store/             # Redux store configuration
│   │   ├── index.js        # Store setup
│   │   ├── cart-slice.js   # Cart state slice
│   │   ├── cart-actions.js # Async cart actions
│   │   └── ui-slice.js     # UI state slice
│   ├── util/              # Utility files
│   │   └── cfg.js         # Configuration (API URL)
│   ├── App.js             # Main application component
│   ├── index.js           # Application entry point
│   └── index.css          # Global styles
├── package.json
└── README.md
```

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in development mode. Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes. You will also see any lint errors in the console.

### `npm test`

Launches the test runner in interactive watch mode. See the [running tests](https://facebook.github.io/create-react-app/docs/running-tests) section for more information.

### `npm run build`

Builds the app for production to the `build` folder. It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes. Your app is ready to be deployed!

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

## State Management

The application uses Redux Toolkit for state management with two main slices:

### Cart Slice (`cart-slice.js`)

Manages shopping cart state:
- `items`: Array of cart items
- `totalQuantity`: Total number of items in cart
- `changed`: Flag indicating if cart has been modified

**Actions:**
- `addItemToCart`: Adds a new item or increments quantity
- `removeItemFromCart`: Removes an item or decrements quantity
- `replaceCart`: Replaces entire cart (used when fetching from backend)

### UI Slice (`ui-slice.js`)

Manages UI state:
- `cartIsVisible`: Controls cart visibility
- `notification`: Notification object with status, title, and message

**Actions:**
- `toggle`: Toggles cart visibility
- `showNotification`: Displays a notification

### Async Actions (`cart-actions.js`)

Handles asynchronous operations:
- `fetchCartData`: Fetches cart data from backend on app load
- `sendCartData`: Saves cart data to backend when cart changes

## Components Overview

### Cart Components

- **Cart**: Main cart container displaying all cart items
- **CartItem**: Individual cart item with quantity controls
- **CartButton**: Header button to toggle cart visibility

### Shop Components

- **Products**: Product listing container
- **ProductItem**: Individual product card with add to cart functionality

### Layout Components

- **Layout**: Main application layout wrapper
- **MainHeader**: Application header with cart button

### UI Components

- **Card**: Reusable card component for content containers
- **Notification**: Toast-style notification component

## API Integration

The application integrates with a REST API for cart persistence:

### Fetch Cart Data

```javascript
GET /cart.json
```

Returns the current cart state from the backend.

### Update Cart Data

```javascript
PUT /cart.json
Body: {
  items: [...],
  totalQuantity: number
}
```

Saves the current cart state to the backend.

The API endpoint is configured in `src/util/cfg.js`. Make sure to update it with your actual backend URL before running the application.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

---

**Note**: Remember to configure your database URL in `src/util/cfg.js` before running the application. The app requires a backend API endpoint for full functionality.
