# LinkUp - Professional Social Network Platform

A modern, responsive social networking platform built for professionals to connect, share ideas, and build meaningful relationships.

## 🚀 Tech Stack

### Frontend
- **Next.js 13** - React framework with App Router
- **React 18** - UI library with hooks
- **Tailwind CSS** - Utility-first CSS framework
- **Lucide React** - Beautiful icons

### Backend & Database
- **Firebase Authentication** - User authentication system
- **Cloud Firestore** - NoSQL database for real-time data
- **Firebase Security Rules** - Database security

### Development Tools
- **TypeScript** - Type safety
- **ESLint** - Code linting
- **PostCSS** - CSS processing

## 📦 Setup Instructions

### Prerequisites
- Node.js 18+ installed
- Firebase project set up

### 1. Clone the Repository
```bash
git clone <your-repository-url>
cd linkup-social-platform
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Firebase Configuration
1. Create a new Firebase project at [Firebase Console](https://console.firebase.google.com)
2. Enable Authentication (Email/Password)
3. Create a Firestore database
4. Update your Firebase config in `firebase/config.js`:

```javascript
const firebaseConfig = {
  apiKey: "your-api-key",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "your-sender-id",
  appId: "your-app-id"
};
```

### 4. Set up Firestore Security Rules
Copy the following rules to your Firestore Security Rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users collection - allow read for all, write for authenticated users on their own data
    match /users/{userId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Posts collection - allow read for all, write for authenticated users
    match /posts/{postId} {
      allow read: if true;
      allow create: if request.auth != null;
      allow update: if request.auth != null;
      allow delete: if request.auth != null && request.auth.uid == resource.data.authorId;
    }
    
    // Comments collection
    match /comments/{commentId} {
      allow read: if true;
      allow create: if request.auth != null;
      allow update: if request.auth != null && request.auth.uid == resource.data.authorId;
      allow delete: if request.auth != null && request.auth.uid == resource.data.authorId;
    }
  }
}
```

### 5. Create Required Firestore Indexes
In your Firebase Console, go to Firestore > Indexes and create:

1. **Posts Collection**:
   - Collection ID: `posts`
   - Fields: `createdAt` (Descending)

2. **Posts by Author**:
   - Collection ID: `posts`
   - Fields: `authorId` (Ascending), `createdAt` (Descending)

### 6. Run the Development Server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 7. Build for Production
```bash
npm run build
```

## ✅ Core Features

### 1. User Authentication
- **Email & Password Registration/Login**: Secure authentication system
- **User Profiles**: Complete profile management with name, email, and bio
- **Profile Customization**: Users can edit their profiles and add personal information

### 2. Public Post Feed
- **Create Posts**: Share text-based thoughts and ideas (up to 500 characters)
- **Read Posts**: View all posts in chronological order
- **Display Posts**: Home feed shows posts with author's name and timestamp
- **Real-time Updates**: Posts appear instantly without page refresh

### 3. Profile Page
- **View User Profile**: See any user's profile with their information
- **User Posts**: View all posts from a specific user
- **Profile Information**: Display name, email, bio, and join date

## 🎨 Additional Features

- **Dark/Light Theme**: Toggle between themes with system preference detection
- **Responsive Design**: Optimized for desktop, tablet, and mobile devices
- **Real-time Interactions**: Like posts and see updates instantly
- **Search Functionality**: Find users by name across the platform
- **Enhanced UI/UX**: Modern design with smooth animations and micro-interactions
- **Post Management**: Users can delete their own posts
- **Comments System**: Add and view comments on posts

## 🏗️ Project Structure

```
linkup-social-platform/
├── components/           # Reusable UI components
│   ├── EnhancedNavbar.js
│   ├── EnhancedPostCard.js
│   ├── EnhancedProfileCard.js
│   ├── PostForm.js
│   └── FeedSidebar.js
├── contexts/            # React contexts
│   └── ThemeContext.js
├── firebase/            # Firebase configuration
│   └── config.js
├── pages/               # Next.js pages
│   ├── _app.js
│   ├── index.js
│   ├── login.js
│   ├── register.js
│   ├── create.js
│   ├── edit-profile.js
│   ├── search.js
│   ├── network.js
│   ├── jobs.js
│   ├── messages.js
│   └── profile/[id].js
├── utils/               # Utility functions
│   ├── auth.js
│   └── protectedRoute.js
├── app/                 # App configuration
│   ├── globals.css
│   └── layout.tsx
└── public/              # Static assets
```

## 🔐 Security Features

- **Authentication Required**: Protected routes require user authentication
- **Data Validation**: Client and server-side validation
- **Firestore Security Rules**: Database-level security
- **User Data Protection**: Users can only modify their own data

## 🚀 Deployment

### Deploy to Netlify
1. Build the project: `npm run build`
2. Deploy the `out` folder to [Netlify](https://netlify.com)
3. Set up environment variables if needed

### Deploy to Vercel (Alternative)
1. Push your code to GitHub
2. Connect your repository to [Vercel](https://vercel.com)
3. Deploy with default settings

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Commit your changes: `git commit -m 'Add new feature'`
4. Push to the branch: `git push origin feature/new-feature`
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- Firebase for backend services
- Tailwind CSS for styling
- Lucide React for icons
- Next.js team for the amazing framework

---

**Built with ❤️ for the professional community**