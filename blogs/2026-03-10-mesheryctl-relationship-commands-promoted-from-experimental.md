---
title: "Mesheryctl Relationship Commands Promoted From Experimental"
url: "https://meshery.io/blog/2026/03/2026-03-10-mesheryctl-relationship-cmds/"
date: "2026-03-10T00:00:00+00:00"
author: "Matthieu Evrin"
feed_url: "https://meshery.io/feed.xml"
---
<p>If you are managing cloud-native infrastructure with Meshery, understanding how your components interact is critical. This post walks you through the <code class="language-plaintext highlighter-rouge">mesheryctl relationship</code> commands and celebrates an important milestone: their <strong>officially graduated from experimental mode</strong>.</p>

<h3 id="from-mesheryctl-exp-relationship-to-mesheryctl-relationship">From <code class="language-plaintext highlighter-rouge">mesheryctl exp relationship</code> to <code class="language-plaintext highlighter-rouge">mesheryctl relationship</code></h3>

<p>After a period of stabilization, community feedback, and real-world usage, <strong>the relationship commands have been promoted to stable</strong> and moved to the top-level namespace:</p>

<table>
  <thead>
    <tr>
      <th>Before (experimental)</th>
      <th>After (stable)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl exp relationship generate</code></td>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl relationship generate</code></td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl exp relationship list</code></td>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl relationship list</code></td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl exp relationship search</code></td>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl relationship search</code></td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl exp relationship view</code></td>
      <td><code class="language-plaintext highlighter-rouge">mesheryctl relationship view</code></td>
    </tr>
  </tbody>
</table>

<blockquote>
  <p><strong>What is a Meshery Relationship?</strong><br />
In the Meshery ecosystem, a <strong>relationship</strong> defines how two or more <a href="https://docs.meshery.io/concepts/logical/components">components</a> are interconnected. Relationships capture the dependencies, policies, and interactions between components within a <a href="https://docs.meshery.io/concepts/logical/models">model</a>. They are organized by <strong>kind</strong> (e.g., <code class="language-plaintext highlighter-rouge">hierarchical</code>, <code class="language-plaintext highlighter-rouge">edge</code>), <strong>type</strong>, and <strong>subtype</strong> (e.g., <code class="language-plaintext highlighter-rouge">parent</code>, <code class="language-plaintext highlighter-rouge">binding</code>) and are evaluated by Meshery’s policy engine to enforce design constraints and visualize architectural intent.<br />
<a href="https://docs.meshery.io/concepts/logical/relationships">Learn more about Meshery Relationships</a></p>
</blockquote>

<p>The <code class="language-plaintext highlighter-rouge">mesheryctl relationship</code> command gives you a convenient CLI interface to interact with the relationships registered in your Meshery Server. It exposes four subcommands — <code class="language-plaintext highlighter-rouge">list</code>, <code class="language-plaintext highlighter-rouge">search</code>, <code class="language-plaintext highlighter-rouge">view</code>, and <code class="language-plaintext highlighter-rouge">generate</code> — each targeting a specific use case.</p>

<hr />

<h2 id="base-command-mesheryctl-relationship">Base command: <code class="language-plaintext highlighter-rouge">mesheryctl relationship</code></h2>

<p><strong>Description:</strong> The root command for managing relationships. On its own, it prints usage information. Combined with the <code class="language-plaintext highlighter-rouge">--count</code> flag, it returns the total number of relationships registered in Meshery Server.</p>

<p><strong>Flags:</strong></p>

<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Short</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--count</code></td>
      <td><code class="language-plaintext highlighter-rouge">-c</code></td>
      <td><code class="language-plaintext highlighter-rouge">false</code></td>
      <td>Get the total number of relationships</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--help</code></td>
      <td><code class="language-plaintext highlighter-rouge">-h</code></td>
      <td> </td>
      <td>Display help for the command</td>
    </tr>
  </tbody>
</table>

<p><strong>Example — display the total count of registered relationships:</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~<span class="nv">$ </span>mesheryctl relationship <span class="nt">--count</span>
Total number of relationships: 597
</code></pre></div></div>

<hr />

<h2 id="mesheryctl-relationship-list"><code class="language-plaintext highlighter-rouge">mesheryctl relationship list</code></h2>

<p><strong>Description:</strong> Lists all relationships registered in Meshery Server, displaying their ID, kind, API version, model name, subtype, and type in a tabular format. Supports paginated output so you can navigate through large sets of results interactively.</p>

<p><strong>Flags:</strong></p>

<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Short</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--page</code></td>
      <td><code class="language-plaintext highlighter-rouge">-p</code></td>
      <td><code class="language-plaintext highlighter-rouge">1</code></td>
      <td>List next set of relationships at the specified page number</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--pagesize</code></td>
      <td> </td>
      <td><code class="language-plaintext highlighter-rouge">10</code></td>
      <td>Number of results per page</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--count</code></td>
      <td><code class="language-plaintext highlighter-rouge">-c</code></td>
      <td><code class="language-plaintext highlighter-rouge">false</code></td>
      <td>Display the total count of relationships only</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--help</code></td>
      <td><code class="language-plaintext highlighter-rouge">-h</code></td>
      <td> </td>
      <td>Display help for the command</td>
    </tr>
  </tbody>
</table>

<p><strong>Example — list all relationships (page 1, 10 results):</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~<span class="nv">$ </span>mesheryctl relationship list
Total number of relationships: 597
Page: 1
ID                                    KIND          API VERSION  MODEL NAME                             SUB TYPE   TYPE
0f9ba842-d709-4d2b-a60e-f4c2b46d02ad  edge          v1.0.0       aws-apigatewayv2-controller            network    non-binding
c360e677-c0e2-4f21-a50f-94c5318a4e21  edge          v1.0.0       aws-apigatewayv2-controller            reference  non-binding
023becab-18f5-4eae-bdd2-1ef03eecffd6  edge          v1.0.0       aws-apigatewayv2-controller            reference  non-binding
7a77e701-bf34-4a07-9aff-41e61b1d87dd  edge          v1.0.0       aws-apigatewayv2-controller            reference  non-binding
13f0e4f2-81f1-4714-b850-88a8fe0d8acd  edge          v1.0.0       aws-apigatewayv2-controller            reference  non-binding
644b97c4-7f9e-41d8-9676-deb34b873cea  hierarchical  v1.0.0       aws-apigatewayv2-controller            inventory  parent
896cb3d1-1b37-47cc-91af-5f9003ef5182  edge          v1.0.0       aws-apigatewayv2-controller            reference  non-binding
343d7ee3-bf0c-41fa-95ad-deb2d6562ba8  edge          v1.0.0       aws-applicationautoscaling-controller  reference  non-binding
ec82ff50-d8dc-4c55-bb0b-a5633546b0ca  edge          v1.0.0       aws-applicationautoscaling-controller  reference  non-binding
b98483ea-b70d-40fd-915f-7e624290cf42  edge          v1.0.0       aws-applicationautoscaling-controller  reference  non-binding
</code></pre></div></div>

<p><strong>Additional usage examples:</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># List relationships on a specific page</span>
mesheryctl relationship list <span class="nt">--page</span> 2

<span class="c"># List relationships with a custom page size</span>
mesheryctl relationship list <span class="nt">--pagesize</span> 25

<span class="c"># Display only the total count of relationships</span>
mesheryctl relationship list <span class="nt">--count</span>
</code></pre></div></div>

<hr />

<h2 id="mesheryctl-relationship-search"><code class="language-plaintext highlighter-rouge">mesheryctl relationship search</code></h2>

<p><strong>Description:</strong> Searches registered relationships used by different models. You can narrow down results by kind, type, subtype, and/or model name. At least one filter flag is required.</p>

<p><strong>Flags:</strong></p>

<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Short</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--kind</code></td>
      <td><code class="language-plaintext highlighter-rouge">-k</code></td>
      <td> </td>
      <td>Search relationships of a particular kind (e.g., <code class="language-plaintext highlighter-rouge">hierarchical</code>, <code class="language-plaintext highlighter-rouge">edge</code>)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--type</code></td>
      <td><code class="language-plaintext highlighter-rouge">-t</code></td>
      <td> </td>
      <td>Search relationships of a particular type</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--subtype</code></td>
      <td><code class="language-plaintext highlighter-rouge">-s</code></td>
      <td> </td>
      <td>Search relationships of a particular subtype (e.g., <code class="language-plaintext highlighter-rouge">parent</code>, <code class="language-plaintext highlighter-rouge">binding</code>)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--model</code></td>
      <td><code class="language-plaintext highlighter-rouge">-m</code></td>
      <td> </td>
      <td>Search relationships belonging to a particular model</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--page</code></td>
      <td><code class="language-plaintext highlighter-rouge">-p</code></td>
      <td><code class="language-plaintext highlighter-rouge">1</code></td>
      <td>Page number of results to fetch</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--help</code></td>
      <td><code class="language-plaintext highlighter-rouge">-h</code></td>
      <td> </td>
      <td>Display help for the command</td>
    </tr>
  </tbody>
</table>

<p><strong>Example — search for hierarchical relationships:</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~<span class="nv">$ </span>mesheryctl relationship search <span class="nt">--kind</span> hierarchical
Total number of relationships: 194
Page: 1
ID                                    KIND          API VERSION  MODEL NAME                    SUB TYPE   TYPE
644b97c4-7f9e-41d8-9676-deb34b873cea  hierarchical  v1.0.0       aws-apigatewayv2-controller   inventory  parent
b236f6ba-60a8-4e5e-a36d-f0c8b2fd87f4  hierarchical  v1.0.0       aws-documentdb-controller     inventory  parent
2efa3365-5e2d-4cd2-a313-408363419d4f  hierarchical  v1.0.0       aws-dynamodb-controller       inventory  parent
4b5fa9d9-80e7-44fa-a563-ad03ef590e83  hierarchical  v1.0.0       aws-ec2-controller            inventory  parent
f5303970-cbde-49f9-9878-4f13f31ec9ff  hierarchical  v1.0.0       aws-ec2-controller            inventory  parent
853279e4-c4b7-4b95-819a-4b3ec14319a4  hierarchical  v1.0.0       aws-ecs-controller            inventory  parent
eb0da592-9e2b-44de-8e4c-457f3743f2a5  hierarchical  v1.0.0       aws-efs-controller            inventory  parent
1a848bd2-14a9-4a4c-a6ff-2dda7116d1d6  hierarchical  v1.0.0       aws-eks-controller            inventory  parent
a933d19d-e447-4e13-a252-eba9451a3a6c  hierarchical  v1.0.0       aws-emrcontainers-controller  inventory  parent
4d6d9799-496a-46b6-84fa-c033f2e85b26  hierarchical  v1.0.0       aws-eventbridge-controller    inventory  parent
</code></pre></div></div>

<p><strong>Additional usage examples:</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># Search by subtype</span>
mesheryctl relationship search <span class="nt">--subtype</span> parent

<span class="c"># Search by model and kind</span>
mesheryctl relationship search <span class="nt">--model</span> kubernetes <span class="nt">--kind</span> edge

<span class="c"># Search with pagination</span>
mesheryctl relationship search <span class="nt">--type</span> binding <span class="nt">--page</span> 2
</code></pre></div></div>

<hr />

<h2 id="mesheryctl-relationship-view"><code class="language-plaintext highlighter-rouge">mesheryctl relationship view</code></h2>

<p><strong>Description:</strong> Views the full definition of a specific relationship belonging to a given model. The command fetches the relationships registered for the model you specify, then presents an interactive selection prompt so you can pick the exact relationship you want to inspect. The output is rendered in YAML format by default, or in JSON if requested. You can also save the output to a file.</p>

<p><strong>Flags:</strong></p>

<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Short</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--output-format</code></td>
      <td><code class="language-plaintext highlighter-rouge">-o</code></td>
      <td><code class="language-plaintext highlighter-rouge">yaml</code></td>
      <td>Format to display in: <code class="language-plaintext highlighter-rouge">json</code> or <code class="language-plaintext highlighter-rouge">yaml</code></td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--save</code></td>
      <td><code class="language-plaintext highlighter-rouge">-s</code></td>
      <td><code class="language-plaintext highlighter-rouge">false</code></td>
      <td>Save the output as a JSON or YAML file</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--help</code></td>
      <td><code class="language-plaintext highlighter-rouge">-h</code></td>
      <td> </td>
      <td>Display help for the command</td>
    </tr>
  </tbody>
</table>

<p><strong>Example — view relationships of the <code class="language-plaintext highlighter-rouge">kubernetes</code> model:</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~<span class="nv">$ </span>mesheryctl relationship view kubernetes
Use ↑/↓/←/→ to navigate, Ctrl+C to cancel
? Select item:
    kind: edge, EvaluationPolicy: , SubType: reference
    kind: edge, EvaluationPolicy: , SubType: firewall
  ▸ kind: edge, EvaluationPolicy: , SubType: firewall
    kind: edge, EvaluationPolicy: , SubType: mount
    kind: edge, EvaluationPolicy: , SubType: mount
↓   kind: edge, EvaluationPolicy: , SubType: mount
</code></pre></div></div>

<details><b>kubernetes example</b>

<div class="highlight">
  <pre class="highlight">
  <code>
id: a12b458d-221a-4559-95c9-b6e6e3f8bf6e
capabilities: null
evaluationQuery: ""
kind: edge
metadata:
    description: ""
    styles:
        primaryColor: ""
        svgColor: ""
        svgWhite: ""
    isAnnotation: false
    additionalproperties: {}
model:
    version: v1.0.0
    name: kubernetes
    displayName: Kubernetes
    id: 00000000-0000-0000-0000-000000000000
    registrant:
        kind: github
    model:
        version: v1.35.0-rc.1
modelid: 00000000-0000-0000-0000-000000000000
schemaVersion: relationships.meshery.io/v1alpha3
selectors:
    - allow:
        from:
            - id: null
              kind: StorageClass
              match:
                from:
                    - id: null
                      kind: self
                      mutatedRef:
                        - - component
                          - kind
                        - - displayName
                to:
                    - id: null
                      kind: PersistentVolumeClaim
                      mutatorRef:
                        - - component
                          - kind
                        - - configuration
                          - spec
                          - storageClassName
              match_strategy_matrix: []
              model:
                version: ""
                name: kubernetes
                displayName: ""
                id: 00000000-0000-0000-0000-000000000000
                registrant:
                    kind: github
                model:
                    version: ""
              patch: null
        to:
            - id: null
              kind: PersistentVolume
              match:
                from:
                    - id: null
                      kind: PersistentVolumeClaim
                      mutatedRef:
                        - - configuration
                          - spec
                          - storageClassName
                        - - configuration
                          - spec
                          - volumeName
                to:
                    - id: null
                      kind: self
                      mutatorRef:
                        - - displayName
                        - - configuration
                          - spec
                          - storageClassName
              match_strategy_matrix: []
              model:
                version: ""
                name: kubernetes
                displayName: ""
                id: 00000000-0000-0000-0000-000000000000
                registrant:
                    kind: github
                model:
                    version: ""
              patch: null
      deny:
        from: []
        to: []
subType: mount
status: enabled
type: binding
version: v1.0.0

  </code>
  </pre>
</div>

</details>

<p><strong>Additional usage examples:</strong></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># View relationships in JSON format</span>
mesheryctl relationship view kubernetes <span class="nt">--output-format</span> json

<span class="c"># View relationships and save the output to a file</span>
mesheryctl relationship view kubernetes <span class="nt">--output-format</span> json <span class="nt">--save</span>
</code></pre></div></div>

<hr />

<h2 id="mesheryctl-relationship-generate"><code class="language-plaintext highlighter-rouge">mesheryctl relationship generate</code></h2>

<p><strong>Description:</strong> Generates a relationships documentation file (JSON format) by reading data from a Google Spreadsheet. This is primarily a maintainer-facing command used to keep the Meshery documentation up to date with the latest relationship definitions. It requires a valid spreadsheet ID and base64-encoded Google API credentials.</p>

<p><strong>Flags:</strong></p>

<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Short</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--spreadsheet-id</code></td>
      <td> </td>
      <td> </td>
      <td><em>(Required)</em> Google Spreadsheet ID containing relationship data</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--spreadsheet-cred</code></td>
      <td> </td>
      <td> </td>
      <td><em>(Required)</em> Base64-encoded Google API credentials</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">--help</code></td>
      <td><code class="language-plaintext highlighter-rouge">-h</code></td>
      <td> </td>
      <td>Display help for the command</td>
    </tr>
  </tbody>
</table>

<p><strong>Example — generate relationship documentation from a spreadsheet:</strong></p>

<p>```shell
~$ mesheryctl relationship generate <br />
    –spreadsheet-id spreadsheet-id <br />
    –spreadsheet-cred $CRED
Relationships data generated in docs/_data/RelationshipsData.json
—</p>

<h2 id="conclusion">Conclusion</h2>

<p>The <code class="language-plaintext highlighter-rouge">mesheryctl relationship</code> commands give you direct CLI access to the relationship layer of the Meshery model ecosystem. Whether you want a quick count of registered relationships, need to search for a specific kind, want to inspect a full relationship definition, or are maintaining the documentation data, there is a subcommand for every need.</p>

<p>As a next step, try combining <code class="language-plaintext highlighter-rouge">search</code> and <code class="language-plaintext highlighter-rouge">view</code> together: use <code class="language-plaintext highlighter-rouge">search</code> to find a relationship relevant to your model, then use <code class="language-plaintext highlighter-rouge">view</code> to inspect its full definition and save it locally for reference.</p>

<p>For more details on how relationships work under the hood, visit the official documentation:</p>

<ul>
  <li><a href="https://docs.meshery.io/concepts/logical/relationships">Meshery Relationships concept</a></li>
  <li><a href="https://docs.meshery.io/reference/mesheryctl/relationship">mesheryctl relationship CLI reference</a></li>
</ul>
