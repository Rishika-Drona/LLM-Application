# LLM Applications

A comprehensive guide to building RAG-based LLM applications for production.


In this guide, we will learn how to:

- 💻 Develop a retrieval augmented generation (RAG) based LLM application from scratch.
- 🚀 Scale the major components (load, chunk, embed, index, serve, etc.) in our application.
- ✅ Evaluate different configurations of our application to optimize for both per-component (ex. retrieval_score) and overall performance (quality_score).
- 🔀 Implement LLM hybrid routing approach to bridge the gap b/w OSS and closed LLMs.
- 📦 Serve the application in a highly scalable and available manner.
- 💥 Share the 1st order and 2nd order impacts LLM applications have had on our products.

<br>
<img width="800" src="https://images.ctfassets.net/xjan103pcp94/7FWrvPPlIdz5fs8wQgxLFz/fdae368044275028f0544a3d252fcfe4/image15.png">

## Setup

### API keys
We'll be using [OpenAI](https://platform.openai.com/docs/models/) to access ChatGPT models like `gpt-3.5-turbo`, `gpt-4`, etc. and [Anyscale Endpoints](https://endpoints.anyscale.com/) to access OSS LLMs like `Llama-2-70b`. Be sure to create your accounts for both and have your credentials ready.

### Compute
<details>
  <summary>Local</summary>
  You could run this on your local laptop but a we highly recommend using a setup with access to GPUs. You can set this up on your own or on [Anyscale](http://anyscale.com/).
</details>

<details open>
  <summary>Anyscale</summary><br>
<ul>
<li>Start a new <a href="https://console.anyscale-staging.com/o/anyscale-internal/workspaces">Anyscale workspace on staging</a> using an <a href="https://instances.vantage.sh/aws/ec2/g3.8xlarge"><code>g3.8xlarge</code></a> head node, which has 2 GPUs and 32 CPUs. We can also add GPU worker nodes to run the workloads faster. If you&#39;re not on Anyscale, you can configure a similar instance on your cloud.</li>
<li>Use the <a href="https://docs.anyscale.com/reference/base-images/ray-262/py39#ray-2-6-2-py39"><code>default_cluster_env_2.6.2_py39</code></a> cluster environment.</li>
<li>Use the <code>us-west-2</code> if you&#39;d like to use the artifacts in our shared storage (source docs, vector DB dumps, etc.).</li>
</ul>

</details>

### Repository
```bash
git config --global user.name <GITHUB-USERNAME>
git config --global user.email <EMAIL-ADDRESS>
```

### Environment

Then set up the environment correctly by specifying the values in your `.env` file,
and installing the dependencies:

```bash
pip install --user -r requirements.txt
export PYTHONPATH=$PYTHONPATH:$PWD
pre-commit install
pre-commit autoupdate
```

### Credentials
```bash
touch .env
# Add environment variables to .env
OPENAI_API_BASE="https://api.openai.com/v1"
OPENAI_API_KEY=""  # https://platform.openai.com/account/api-keys
ANYSCALE_API_BASE="https://api.endpoints.anyscale.com/v1"
ANYSCALE_API_KEY=""  # https://app.endpoints.anyscale.com/credentials
DB_CONNECTION_STRING="dbname=postgres user=postgres host=localhost password=postgres"
source .env
```


