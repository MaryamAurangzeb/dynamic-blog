# dynamic-blog

Milestone 3: Assignments Breakdown
Objective: Build a dynamic blog application using Next.js and React, focusing on routing and state management.

1. Dynamic Blog with Multiple Posts
Key Steps:

Set Up the Project:
Create a new Next.js app and configure routing for dynamic pages.

bash
Copy code
npx create-next-app@latest dynamic-blog
cd dynamic-blog
Create a Blog Data File:
Add a data.js file to store mock blog post data.

Example data.js:

javascript
Copy code
export const posts = [
  { id: '1', title: 'Getting Started with Next.js', content: 'This is the content for post 1...' },
  { id: '2', title: 'Understanding React State', content: 'This is the content for post 2...' },
  { id: '3', title: 'Building with Tailwind CSS', content: 'This is the content for post 3...' },
];
Dynamic Routing for Blog Posts:
Create a dynamic route file pages/blog/[id].js.

Example:

jsx
Copy code
import { useRouter } from 'next/router';
import { posts } from '../../data';

const BlogPost = () => {
  const { query } = useRouter();
  const post = posts.find((p) => p.id === query.id);

  if (!post) return <h1>Post Not Found</h1>;

  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">{post.title}</h1>
      <p className="mt-4">{post.content}</p>
    </div>
  );
};

export default BlogPost;
List All Posts on the Homepage:
Create a page at pages/index.js to list and link to individual posts.

Example:

jsx
Copy code
import Link from 'next/link';
import { posts } from './data';

export default function Home() {
  return (
    <div className="p-4">
      <h1 className="text-3xl font-bold mb-4">Blog Posts</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id} className="mb-2">
            <Link href={`/blog/${post.id}`} className="text-blue-600 underline">
              {post.title}
            </Link>
          </li>
        ))}
      </ul>
    </div>
  );
}
2. Implement a Comments Section Using React State
Key Steps:

Add a Comments Section:
Extend pages/blog/[id].js to include a form for adding comments.

Example:

jsx
Copy code
import { useState } from 'react';
import { useRouter } from 'next/router';
import { posts } from '../../data';

const BlogPost = () => {
  const { query } = useRouter();
  const post = posts.find((p) => p.id === query.id);
  const [comments, setComments] = useState([]);
  const [newComment, setNewComment] = useState('');

  if (!post) return <h1>Post Not Found</h1>;

  const addComment = () => {
    if (newComment.trim()) {
      setComments([...comments, newComment]);
      setNewComment('');
    }
  };

  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold">{post.title}</h1>
      <p className="mt-4">{post.content}</p>

      <div className="mt-8">
        <h2 className="text-xl font-semibold">Comments</h2>
        <ul className="mt-4">
          {comments.map((comment, index) => (
            <li key={index} className="border-b py-2">
              {comment}
            </li>
          ))}
        </ul>
        <div className="mt-4">
          <textarea
            value={newComment}
            onChange={(e) => setNewComment(e.target.value)}
            className="w-full border rounded p-2"
            placeholder="Add a comment..."
          />
          <button
            onClick={addComment}
            className="mt-2 bg-blue-600 text-white py-2 px-4 rounded"
          >
            Post Comment
          </button>
        </div>
      </div>
    </div>
  );
};

export default BlogPost;
Deliverables
A homepage that dynamically lists blog posts with links to individual pages.
A dynamic blog post page with:
Content displayed from data.js.
A comments section that uses React state to manage comments.
Deployment
Deploy the project on Vercel:

Push the project to a GitHub repository.
Connect the repository to Vercel and deploy
