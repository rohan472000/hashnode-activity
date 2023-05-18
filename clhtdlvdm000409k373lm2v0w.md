---
title: "Improving CLI Usability in Airflow"
datePublished: Thu May 18 2023 16:58:40 GMT+0000 (Coordinated Universal Time)
cuid: clhtdlvdm000409k373lm2v0w
slug: improving-cli-usability-in-airflow
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684429086999/06636c97-86ae-42f7-b18d-1b091edcd07b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1684429102449/3a0c7149-b763-4397-90fc-781691c26b76.png
tags: github, python, opensource, community, apache-airflow

---

### Introduction:

In the world of open source, I recently had an exciting opportunity to contribute to the Airflow project, an essential tool for orchestrating and scheduling data workflows. During my contribution, I encountered an issue related to the `--state` CLI flag in the `airflow dags list-jobs` command. In this blog post, I want to share my experience and the steps I took to enhance the CLI usability.

### The Problem:

The `--state` flag lacked information about the available arguments it could accept. This meant that users were left in the dark, unsure of what values they could pass in. To make the Airflow CLI more user-friendly, I aimed to provide suggestions for valid state arguments.

### Proposed Solution:

To address this issue, I suggested adding keyword arguments to the `--state` flag, which would guide users on the acceptable state values. I modified the code as follows:

```python
dagrun_states = tuple(state.value for state in DagRunState)
ARG_STATE = Arg(
  ("--state",),
  help="Only list the dag runs corresponding to the state",
  metavar=", ".join(dagrun_states),
  choices=dagrun_states,
)
```

By dynamically generating the `metavar` and `choices` based on the available `DagRunState` values, users would receive auto-suggestions for valid states when using the CLI. This improvement not only enhances the usability of the `list-jobs` command but also reduces the effort required for users to determine the acceptable state arguments on their own.

### Conclusion:

Contributing to open-source projects like Airflow has been an incredible learning experience for me. It allows me to give back to the community and help make the tools we use better for everyone. I encourage you to consider contributing to open-source projects as well. It not only sharpens your skills but also enables you to connect with like-minded individuals who share your passion for technology and collaboration.

Stay tuned for more exciting open-source adventures, and don't forget to connect with me on LinkedIn to join the conversation!

Happy coding and contributing!

Issue Link: [https://github.com/apache/airflow/pull/31308#event-9278550761](https://github.com/apache/airflow/pull/31308#event-9278550761)

LinkedIn: [https://www.linkedin.com/in/rohan-4-anand/](https://www.linkedin.com/in/rohan-4-anand/)