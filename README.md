/*
Project: GitHub Profile README Generator
Description: A React-based interactive UI tool allowing users to input personal information and preferences to dynamically generate a GitHub Profile README.md file with the “Hi there” template.
Built with: React, Tailwind CSS, shadcn/ui, lucide-react
Structure:
  ├── public
  │   └── index.html
  ├── src
  │   ├── components
  │   │   ├── Form.jsx
  │   │   └── Preview.jsx
  │   ├── App.jsx
  │   ├── index.css
  │   └── main.jsx
  ├── package.json
  ├── tailwind.config.js
  └── postcss.config.js
*/

// ===== public/index.html =====
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>GitHub Profile README Generator</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>

// ===== src/main.jsx =====
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './index.css';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// ===== src/index.css =====
@tailwind base;
@tailwind components;
@tailwind utilities;

// ===== tailwind.config.js =====
module.exports = {
  content: [
    './index.html',
    './src/**/*.{js,jsx,ts,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};

// ===== postcss.config.js =====
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};

// ===== package.json =====
{
  "name": "github-profile-readme-generator",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "lucide-react": "^0.263.0",
    "@shadcn/ui": "^1.0.0",
    "react-markdown": "^8.0.0"
  },
  "devDependencies": {
    "vite": "^4.0.0",
    "tailwindcss": "^3.0.0",
    "postcss": "^8.0.0",
    "autoprefixer": "^10.0.0"
  },
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}

// ===== src/App.jsx =====
import React, { useState } from 'react';
import Form from './components/Form';
import Preview from './components/Preview';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Button } from '@/components/ui/button';

export default function App() {
  const [data, setData] = useState({
    working: '',
    learning: '',
    collaborating: '',
    help: '',
    ask: '',
    contact: '',
    pronouns: '',
    funFact: ''
  });

  const [markdown, setMarkdown] = useState('');

  const generateReadme = () => {
    const md = `## Hi there 👋

<!--
**USERNAME/USERNAME** is a ✨ _special_ ✨ repository because its \`README.md\` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ${data.working}
- 🌱 I’m currently learning ${data.learning}
- 👯 I’m looking to collaborate on ${data.collaborating}
- 🤔 I’m looking for help with ${data.help}
- 💬 Ask me about ${data.ask}
- 📫 How to reach me: ${data.contact}
- 😄 Pronouns: ${data.pronouns}
- ⚡ Fun fact: ${data.funFact}
-->
`;
    setMarkdown(md);
  };

  return (
    <div className="min-h-screen bg-gray-50 p-4">
      <Card className="max-w-4xl mx-auto">
        <CardHeader>
          <CardTitle className="text-2xl">GitHub Profile README Generator</CardTitle>
        </CardHeader>
        <CardContent>
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <Form data={data} setData={setData} />
            <div className="flex flex-col">
              <div className="flex-1 overflow-auto border rounded p-4 bg-white">
                <Preview markdown={markdown} />
              </div>
              <Button onClick={generateReadme} className="mt-4 self-end">
                Generate README
              </Button>
            </div>
          </div>
        </CardContent>
      </Card>
    </div>
  );
}

// ===== src/components/Form.jsx =====
import React from 'react';
import { Input } from '@/components/ui/input';
import { Textarea } from '@/components/ui/textarea';
import { Label } from '@/components/ui/label';

export default function Form({ data, setData }) {
  const handleChange = (e) => {
    setData({ ...data, [e.target.name]: e.target.value });
  };

  return (
    <div className="space-y-4">
      <div>
        <Label>Currently Working On</Label>
        <Input name="working" value={data.working} onChange={handleChange} placeholder="e.g., my next web app" />
      </div>
      <div>
        <Label>Currently Learning</Label>
        <Input name="learning" value={data.learning} onChange={handleChange} placeholder="e.g., GraphQL" />
      </div>
      <div>
        <Label>Looking to Collaborate On</Label>
        <Input name="collaborating" value={data.collaborating} onChange={handleChange} placeholder="e.g., open source projects" />
      </div>
      <div>
        <Label>Looking for Help With</Label>
        <Input name="help" value={data.help} onChange={handleChange} placeholder="e.g., Docker" />
      </div>
      <div>
        <Label>Ask Me About</Label>
        <Input name="ask" value={data.ask} onChange={handleChange} placeholder="e.g., JavaScript, React" />
      </div>
      <div>
        <Label>How to Reach Me</Label>
        <Input name="contact" value={data.contact} onChange={handleChange} placeholder="Email, LinkedIn" />
      </div>
      <div>
        <Label>Pronouns</Label>
        <Input name="pronouns" value={data.pronouns} onChange={handleChange} placeholder="e.g., he/him, she/her" />
      </div>
      <div>
        <Label>Fun Fact</Label>
        <Input name="funFact" value={data.funFact} onChange={handleChange} placeholder="A random fun fact about you" />
      </div>
    </div>
  );
}

// ===== src/components/Preview.jsx =====
import React from 'react';
import ReactMarkdown from 'react-markdown';

export default function Preview({ markdown }) {
  return (
    <div className="prose max-w-none">
      {markdown ? <ReactMarkdown>{markdown}</ReactMarkdown> : <p className="text-gray-500">Fill in the fields and click "Generate README" to preview your GitHub Profile README.</p>}
    </div>
  );
}
