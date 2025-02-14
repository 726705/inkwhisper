import React from "react";
import { BrowserRouter as Router, Route, Routes, Link, useParams } from "react-router-dom";
import { Card, CardContent } from "@/components/ui/card";

const stories = [
  { id: 1, title: "The Mysterious Night", excerpt: "A thrilling tale of mystery...", content: "Full story content here..." },
  { id: 2, title: "Echoes of the Past", excerpt: "A journey through time...", content: "Full story content here..." },
];

const Home = () => (
  <div className="p-6">
    <h1 className="text-3xl font-bold mb-4">Welcome to My Stories</h1>
    <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
      {stories.map((story) => (
        <Card key={story.id} className="p-4">
          <CardContent>
            <h2 className="text-xl font-semibold">{story.title}</h2>
            <p className="text-gray-600">{story.excerpt}</p>
            <Link to={`/story/${story.id}`} className="text-blue-500">Read More</Link>
          </CardContent>
        </Card>
      ))}
    </div>
  </div>
);

const StoryPage = () => {
  const { id } = useParams();
  const story = stories.find((s) => s.id === Number(id));
  return story ? (
    <div className="p-6">
      <h1 className="text-3xl font-bold">{story.title}</h1>
      <p className="mt-4">{story.content}</p>
      <Link to="/" className="text-blue-500 mt-4 block">Back to Home</Link>
    </div>
  ) : (
    <p className="p-6">Story not found.</p>
  );
};

const App = () => (
  <Router>
    <nav className="p-4 bg-gray-200 flex gap-4">
      <Link to="/" className="text-blue-600">Home</Link>
    </nav>
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/story/:id" element={<StoryPage />} />
    </Routes>
  </Router>
);

export default App;

