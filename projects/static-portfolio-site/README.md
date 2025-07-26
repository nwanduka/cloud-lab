# 🌐 Static Portfolio Website (Cloud-Hosted on AWS S3)

A personal portfolio website built as my first hands-on cloud engineering project. Rather than only taking courses, I wanted to understand cloud concepts by building something real and figuring things out as I went.

**Live Site:** [victorianduka.com](http://victorianduka.com)  
**Built with:** Jekyll, AWS S3, Route 53  
**Deployment:** Static site hosting with custom domain

## 🛠️ My Approach

After some research about static websites and hosting, I knew I needed to do two things:

### 1. **Build the actual website**
I didn’t want to spend too much time learning HTML, CSS, and JavaScript. My focus was on the **cloud** part of the project. So after some research, I found I could use **Jekyll**, a static site generator that lets you build a full website using templates and Markdown.

- I chose a default Jekyll theme
- Followed the installation and setup guide
- Ran it locally to test (`jekyll serve`)
- Built the static files (`jekyll build`) — this created the `_site` folder with the final version of my website

### 2. **Put the site online (Hosting)**

I learned that **hosting** means storing your website files on a server so people can access them online. Since I’m focused on cloud skills, I chose **AWS S3** for hosting.

Here’s how I went about it:

#### ✅ Created an S3 bucket
At first, I used `victoria-portfolio` for my bucket name. But I later learned that if I want to use a **custom domain**, my bucket name needs to exactly match that domain.

So I:
- Created a new bucket named `victorianduka.com` (I had registered this domain name some months ago on Namecheap).
- Moved the contents of `_site/` into that bucket (⚠️ not the folder itself — just its contents)
- Deleted the old bucket

#### ✅ Enabled Static Website Hosting
I turned on static hosting for the bucket and added a **bucket policy** to allow public read access.

#### ✅ Set up my custom domain
I already owned `victorianduka.com` (registered through Namecheap). Now I needed to connect it to my S3-hosted site.

I had two options:
1. Use AWS Route 53 to manage DNS directly  
2. Keep DNS with Namecheap and use CloudFront (AWS CDN) in front of S3

I chose to use Route 53 because:
- I wanted everything in one place for easier management
- Route 53 integrates well with other AWS services (since I was already hosting on S3 which is an AWS service)
- It’s a good chance to learn about DNS concepts — an important cloud skill

So I:
- Created a Route 53 Hosted Zone
- Updated the nameservers on Namecheap to point to Route 53
- Created DNS records (`A` and `CNAME`) that pointed to the S3 website endpoint

## 🔍 Summary of Key Learnings

- I now understand how static websites work — they’re just files!
- Hosting means putting those files on a server (like S3) so others can access them
- Jekyll helped me generate the site quickly so I could focus on cloud deployment
- AWS S3, Route 53, and domain configuration gave me real-world experience
- I learned how small configuration mistakes (like wrong bucket names or folder structures) can affect the entire setup
- Most importantly, I learned by doing — breaking things, fixing them, and documenting them.

## 📂 Project Files
```
portfolio-website/
├── _config.yml          # Jekyll configuration
├── index.md             # Homepage content
├── about.md             # About page
├── writing.md           # Writing portfolio links
├── _site/               # Generated static files (deployed to S3)
└── README.md           # This documentation
```

## 🔧 What’s Next

This project is still a work in progress. Here are the next steps I plan to take:

### 1. Enable HTTPS with CloudFront + SSL Certificate

Currently, the site is only accessible over `http://`, which isn't secure. To fix that, I plan to integrate **Amazon CloudFront** in front of the S3 bucket and enable **HTTPS** using an SSL certificate issued via **AWS Certificate Manager (ACM)**.

🛑 **Current blocker:** My AWS account is pending full verification and can't create CloudFront distributions yet. I've opened a support ticket with AWS and will update this repo as soon as it's resolved.

🧠 **What I'll gain:**
- Learn how CDNs improve performance and security
- Understand CloudFront behavior with static websites
- Set up and manage SSL certificates with ACM
- Improve user trust and professionalism with HTTPS

### 2. Add a Contact Form (Using AWS Lambda)

I plan to add a simple contact form to make the site feel more interactive. Rather than relying on a third-party service like Formspree or Netlify Forms, I’ll be building the backend myself using AWS Lambda. I’m not entirely sure how I’ll pull it off just yet, but I’m confident that with some research and hands-on experimentation, I’ll figure it out.


