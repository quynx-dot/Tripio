# Tripio

A full-stack MVC travel listing application built with Node.js, Express, and MongoDB. Users can browse property listings, create their own, leave star ratings and reviews, and manage their bookings through a session-based authentication system.

**Live demo:** [tripio-1.onrender.com](https://tripio-1.onrender.com)
**Repo:** [github.com/quynx-dot/Tripio](https://github.com/quynx-dot/Tripio)

---

## Features

- **Listings CRUD** — create, view, edit, and delete property listings with image uploads
- **Image storage on AWS S3** — listing images are uploaded directly to an S3 bucket via `multer-s3`
- **Reviews & ratings** — authenticated users can leave star ratings (via Starability) and text reviews on any listing
- **Authentication & authorization** — signup/login/logout with `passport-local`, session persistence via `connect-mongo`, and ownership checks so only a listing's owner can edit/delete it, and only a review's author can delete it
- **Server-side validation** — request bodies validated with Joi schemas before hitting the database
- **Flash messaging** — success/error feedback on actions via `connect-flash`
- **Responsive UI** — Bootstrap 5 + custom CSS, EJS templating with `ejs-mate` for layout inheritance

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Framework | Express.js |
| Templating | EJS + ejs-mate |
| Database | MongoDB (Atlas) via Mongoose |
| File Storage | AWS S3 (`@aws-sdk/client-s3`, `multer-s3`) |
| Auth | Passport.js (`passport-local`, `passport-local-mongoose`) |
| Sessions | `express-session` + `connect-mongo` |
| Validation | Joi |
| Styling | Bootstrap 5, custom CSS |
| Deployment | Render |

## Project Structure

```
Tripio/
├── controllers/      # Route handler logic (listings, reviews, users)
├── init/              # DB seed script and sample data
├── models/            # Mongoose schemas (Listing, Review, User)
├── public/            # Static assets (CSS, JS)
├── routes/            # Express routers
├── utils/             # Error handling helpers
├── views/             # EJS templates
├── app.js             # App entry point
├── middleware.js       # Auth/ownership/validation middleware
├── schema.js           # Joi validation schemas
└── s3Config.js          # AWS S3 + multer storage config
```

## Getting Started

### Prerequisites

- Node.js v18+
- A MongoDB Atlas cluster (or local MongoDB instance)
- An AWS account with an S3 bucket and an IAM user with S3 access

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/quynx-dot/Tripio.git
   cd Tripio
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Create a `.env` file in the project root with the following variables:

   ```env
   ATLASDB_URL=your_mongodb_connection_string
   SECRET=your_session_secret

   AWS_ACCESS_KEY_ID=your_aws_access_key
   AWS_SECRET_ACCESS_KEY=your_aws_secret_key
   AWS_REGION=ap-south-1
   AWS_BUCKET_NAME=your_s3_bucket_name
   ```

4. Start the app:

   ```bash
   npm start
   ```

   Or, for auto-restart on file changes during development (requires `nodemon` installed globally):

   ```bash
   nodemon app.js
   ```

5. Visit [http://localhost:8080](http://localhost:8080) (or the port Render assigns in production).

## Environment Variables

| Variable | Description |
|---|---|
| `ATLASDB_URL` | MongoDB connection string (Atlas or local) |
| `SECRET` | Secret used to sign session cookies and the Mongo session store |
| `AWS_ACCESS_KEY_ID` | IAM user access key for S3 |
| `AWS_SECRET_ACCESS_KEY` | IAM user secret key for S3 |
| `AWS_REGION` | AWS region the S3 bucket lives in |
| `AWS_BUCKET_NAME` | Name of the S3 bucket used for image uploads |
| `PORT` | (Set automatically by Render in production) |

## Deployment

The app is deployed on [Render](https://render.com). It binds to `process.env.PORT` at runtime (required for Render's dynamic port assignment) and reads all secrets from Render's Environment tab rather than a committed `.env` file.

## Author

Janhavi Ghanghav — [GitHub](https://github.com/quynx-dot)