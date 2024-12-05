---
title: "What is Function Calling?"
date: 2021-12-18T11:10:36+08:00
draft: false
language: en
description: Explanation of Function Calling
---

Function calling, also known as tool use in ML, is a powerful feature that allows large language models (LLMs) to interact with external tools, APIs, and systems in order to perform specific tasks beyond their their basic inference capabilities. This feature extends the functionality of LLMs by enabling them to execute actions, retrieve real-time data, and interact dynamically with other systems, significantly enhancing their versatility and problem-solving capabilities.

The process of function calling typically involves several steps. First, the LLM detects that a user query or task requires an action it cannot perform on its own. It then identifies the appropriate function or API to fulfill the request and sends the necessary parameters to the external agent. The external agent then processes the request and returns the results, which the LLM then integrates into its response to the user. This allows LLMs to perform a wide range of tasks, such as retrieving real-time weather information, processing payments, or even controlling IoT devices.

Function calling addresses some key limitations of traditional AI models. It allows models to access up-to-date real time information and interact with external data sources. This not only helps expand the models' "knowledge" beyond their training datasets but also improves upon RAG models by giving LLMs access to real time data instead of static vector stores. Additionally, by offloading certain tasks to external functions, LLMs can provide more accurate, contextually relevant responses and execute real-world actions through function calling. Below is a demo of function calling in action:

<iframe width="560" height="315" src="https://www.youtube.com/embed/46ICvnWhcpk?si=JpdTxKFUdvX5oIK3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
