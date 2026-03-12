---
layout: single
title: "Huffman Compression Web APP"
date: 2024-12-31
permalink: /project-neuHuffman/
categories:
  - Projects
excerpt: "Using basic C++ to build the server for Huffman compression graphical system"
header:
  teaser: "assets/images/huffman.jpg" 
---
The Huffman compression software is a two-week course design project at Northeastern University. It uses pure standard C++ libraries to build the server and the encoding/decoding logic. JavaScript is used for frontend communication and display logic, supplemented by HTML and CSS for web structuring and styling.
<div style="text-align: center; margin-bottom: 1em; margin-top: 1em;">
  <img 
      src="/assets/images/huffmanLogic.png" 
      alt="Huffman Logic" 
      style="max-width: 100%; height: auto; border-radius: 8px;" 
    />
</div>
This diagram shows the overall logic of the Huffman software.
In fact, the Huffman encoding and decoding process is the simplest part of this project. It only requires converting the content (whether it's text, images, or files) into Base64 encoding, and then storing it via Huffman encoding. Decoding represents the exact opposite. Writing the server and transmission logic using the C++ standard library is the most headache-inducing part. During the development of the project, information from the transmission stream was completely parsed using the `string` library to decompose HTTP headers and relevant content (by finding the start and end positions for truncation). Not to mention manually constructing JSON formats using strings, and handling Chinese characters and special characters (like `/`, `'`, `"`, etc.). In the phase of writing the server logic, we had to manually set the buffer size and write the buffering, looping, and concatenation logic for data transmission, so that data could be completely transmitted (since it needed to support up to 10MB image transmission), while ensuring that excessively large data wouldn't clog the transmission stream and cause low-level errors.