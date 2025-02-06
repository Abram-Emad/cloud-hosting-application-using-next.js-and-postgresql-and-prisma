# Cloud Hosting Application

A full-stack cloud hosting platform built with Next.js, PostgreSQL, and Prisma. This application provides a user-friendly interface for managing cloud services, user authentication, and real-time data interaction.

## Features

- **User Authentication**: Secure sign-up/login using NextAuth with GitHub, Google, and email/password.
- **Dashboard**: Interactive dashboard for managing cloud services, viewing usage statistics, and billing.
- **Service Management**: Create, update, or delete cloud services (e.g., virtual machines, storage).
- **Responsive Design**: Built with Tailwind CSS for seamless mobile and desktop experiences.
- **Database Integration**: PostgreSQL database managed via Prisma ORM for robust data handling.
- **API Routes**: Next.js API routes for handling backend logic securely.

## Technologies Used

- **Frontend**: Next.js (React), Tailwind CSS
- **Backend**: Next.js API Routes
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Authentication**: NextAuth.js
- **Deployment**: Vercel (Frontend/Backend), Railway/Heroku (PostgreSQL)
- **Version Control**: Git, GitHub

## Installation

Follow these steps to run the project locally:

### Prerequisites

- Node.js v16+ and npm/yarn
- PostgreSQL database (local or remote)
- GitHub/Google OAuth credentials (for authentication)

### Steps

1. **Clone the Repository**
   bash
   git clone https://github.com/Abram-Emad/cloud-hosting-application-using-next.js-and-postgresql-and-prisma.git
   cd cloud-hosting-application-using-next.js-and-postgresql-and-prisma
   

2. **Install Dependencies**
   bash
   npm install
   # or
   yarn install
   

3. **Environment Setup**
   - Create a `.env.local` file in the root directory:
     env
     DATABASE_URL="postgresql://user:password@localhost:5432/db_name"
     NEXTAUTH_SECRET="your-secure-secret"
     GITHUB_ID="your-github-oauth-id"
     GITHUB_SECRET="your-github-oauth-secret"
     GOOGLE_ID="your-google-oauth-id"
     GOOGLE_SECRET="your-google-oauth-secret"
     

4. **Database Setup**
   - Run Prisma migrations:
     bash
     npx prisma migrate dev --name init
     
   - Generate Prisma Client:
     bash
     npx prisma generate
     

5. **Start the Development Server**
   bash
   npm run dev
   # or
   yarn dev
   
   Visit `http://localhost:3000` in your browser.

## Configuration

### Prisma Schema
The database schema is defined in `prisma/schema.prisma`. Example snippet:
prisma
model User {
  id            String    @id @default(uuid())
  name          String?
  email         String?   @unique
  emailVerified DateTime?
  services      Service[]
}

model Service {
  id          String   @id @default(uuid())
  name        String
  description String
  userId      String
  user        User     @relation(fields: [userId], references: [id])
}


### Authentication
Configure providers in `pages/api/auth/[...nextauth].js`. Example:
javascript
import NextAuth from "next-auth";
import GitHubProvider from "next-auth/providers/github";

export default NextAuth({
  providers: [
    GitHubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
    // Add other providers here
  ],
});


## Project Structure


- ├── components/       # Reusable React components
- ├── pages/            # Next.js pages and API routes
- │   ├── api/          # Backend API endpoints
- │   └── dashboard/    # User dashboard page
- ├── prisma/           # Prisma schema and migrations
- ├── styles/           # Global CSS/Tailwind styles
- ├── .env.local        # Environment variables
- └── package.json      # Project dependencies


## Deployment

### Vercel (Frontend/Backend)
1. Push your code to a GitHub repository.
2. Import the repo into Vercel and configure environment variables.
3. Deploy! Next.js API routes are automatically hosted as serverless functions.

### PostgreSQL (Database)
1. Use a managed service like [Railway](https://railway.app) or Neon.tech.
2. Update the `DATABASE_URL` in `.env.local` with your production database URL.

## Contributing

Contributions are welcome! Follow these steps:
1. Fork the repository.
2. Create a feature branch: `git checkout -b feat/your-feature`.
3. Commit changes: `git commit -m "Add your feature"`.
4. Push to the branch: `git push origin feat/your-feature`.
5. Open a Pull Request.

## License

Distributed under the MIT License. See `LICENSE` for details.

## Acknowledgements

- [Next.js Documentation](https://nextjs.org/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## FAQ

**Q: How do I reset the database?**  
A: Run `npx prisma migrate reset` to wipe and recreate the database schema.

**Q: Can I use a different database?**  
A: Yes! Prisma supports MySQL, SQLite, and more. Update `DATABASE_URL` and `schema.prisma` accordingly.

**Q: Authentication isn't working. What should I check?**  
A: Ensure OAuth credentials are correctly set in `.env.local` and CORS settings are configured.

---

**Contact**  
Abram Emad - [GitHub Profile](https://github.com/Abram-Emad)  
Project Link: [https://github.com/Abram-Emad/cloud-hosting-application-using-next.js-and-postgresql-and-prisma](https://github.com/Abram-Emad/cloud-hosting-application-using-next.js-and-postgresql-and-prisma)
