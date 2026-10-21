# 🎵 Band Wordle

A daily Wordle game themed around music and band instruments, featuring a rotating word list, leaderboards, and Supabase integration.

## 🎮 Features

- **Daily Word Rotation**: 6-letter words rotate daily based on the date (weekdays only; no puzzle on weekends or Labor Day)
- **Band/Music Theme**: ~30 music-related words (instruments, genres, terms)
- **Standard Wordle Rules**: 6 guesses, colored feedback tiles
- **Leaderboards**: Daily (fewest guesses) and monthly (most games solved, then fewest total guesses) rankings
- **Score Submission**: Players can submit scores with nickname and section
- **Mobile-Friendly**: Responsive design with Tailwind CSS
- **Supabase Backend**: Free database hosting

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ 
- npm or yarn
- Supabase account (free)

### 1. Install Dependencies
```bash
npm install
```

### 2. Set Up Environment Variables
Create a `.env` file in the root directory:
```bash
VITE_SUPABASE_URL=your_supabase_project_url_here
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key_here
```

### 3. Run Locally
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

## 🗄️ Supabase Setup

### 1. Create Supabase Project
1. Go to [supabase.com](https://supabase.com)
2. Sign up/login and create a new project
3. Wait for the project to be ready

### 2. Create Database Table
Run this SQL in your Supabase SQL Editor:

```sql
-- Create the scores table
CREATE TABLE scores (
  id BIGSERIAL PRIMARY KEY,
  nickname TEXT NOT NULL,
  section TEXT NOT NULL,
  guesses INTEGER NOT NULL,
  solved BOOLEAN NOT NULL,
  date DATE NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Create unique constraint to prevent multiple submissions per user per day
CREATE UNIQUE INDEX unique_user_date ON scores (nickname, date);

-- Enable Row Level Security (RLS)
ALTER TABLE scores ENABLE ROW LEVEL SECURITY;

-- Create policy to allow all operations (for demo purposes)
-- In production, you might want to restrict this
CREATE POLICY "Allow all operations" ON scores FOR ALL USING (true);
```

### 3. Get API Keys
1. Go to Project Settings → API
2. Copy the Project URL and anon public key
3. Add them to your `.env` file

## 🌐 Deployment

### Option 1: Netlify (Recommended)
1. Push your code to GitHub
2. Go to [netlify.com](https://netlify.com)
3. Click "New site from Git"
4. Connect your GitHub repository
5. Build command: `npm run build`
6. Publish directory: `dist`
7. Add environment variables in Site Settings → Environment Variables

### Option 2: Vercel
1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Click "New Project"
4. Import your GitHub repository
5. Vercel will auto-detect Vite settings
6. Add environment variables in Project Settings → Environment Variables

## 📱 Game Rules

- **Objective**: Guess the 6-letter word in 6 attempts
- **Feedback**:
  - 🟩 Green: Letter is correct and in right position
  - 🟨 Yellow: Letter is in word but wrong position
  - ⬛ Gray: Letter is not in word
- **Daily Word**: Same word for all players each day
- **Scoring**: Fewer guesses = better score
- **Submission**: One score per nickname per day

## 🎯 Word Categories

The game includes ~30 music-related words, for example:
- **Instruments**: GUITAR, GIBSON, FLUTES
- **Music Terms**: RHYTHM, MELODY, TREBLE, OCTAVE, LEGATO, SONATA
- **Genres**: REGGAE, TECHNO, BALLAD, ANTHEM
- **Band Related**: CHORUS, ENCORE, STUDIO, TUNING, UNISON

## 🔧 Customization

### Adding More Words
Edit `src/wordList.js` to add your own words. Make sure they are:
- Exactly 6 letters long
- All uppercase
- Music/band related

### Styling
The game uses Tailwind CSS. Custom styles are in `src/index.css` with the `@layer components` directive.

### Database Schema
Modify the Supabase table structure in the SQL setup above if you need additional fields.

## 🐛 Troubleshooting

### Common Issues

1. **Environment Variables Not Working**
   - Ensure `.env` file is in the root directory
   - Restart the dev server after adding variables
   - Check that variable names start with `VITE_`

2. **Supabase Connection Errors**
   - Verify your URL and API key are correct
   - Check that your Supabase project is active
   - Ensure the `scores` table exists

3. **Build Errors**
   - Clear `node_modules` and reinstall: `rm -rf node_modules && npm install`
   - Check Node.js version: `node --version`

### Development Tips

- Use browser dev tools to check for console errors
- Check the Network tab for API call failures
- Verify Supabase policies allow the operations you need

## 📄 License

This project is open source and available under the MIT License.

## 🤝 Contributing

Feel free to submit issues, feature requests, or pull requests to improve the game!

---

**Happy Wordling! 🎵🎮**
