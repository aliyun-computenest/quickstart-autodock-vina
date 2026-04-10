<h1>AutoDock Vina EHPC Compute Nest Quick Deployment</h1>

<blockquote>
    <p><strong>Disclaimer:</strong> This service is provided by a third party. We strive to ensure its security, accuracy, and reliability, but we cannot guarantee that it will be completely free from failures, interruptions, errors, or attacks. Therefore, the company hereby declares: it makes no representations, warranties, or commitments regarding the content, accuracy, completeness, reliability, applicability, or timeliness of this service, and assumes no liability for any direct or indirect losses or damages arising from your use of this service; it assumes no liability for the content, accuracy, completeness, reliability, applicability, or timeliness of third-party websites, applications, products, and services accessed by you through this service, and you shall bear the risks and responsibilities arising from the consequences of use; it assumes no liability for any losses or damages arising from your use of this service, including but not limited to direct losses, indirect losses, loss of profits, loss of goodwill, loss of data, or other economic losses, even if the company has been informed in advance of the possibility of such losses or damages; we reserve the right to modify this disclaimer from time to time, so please check this disclaimer regularly before using this service. If you have any questions or doubts about this disclaimer or this service, please contact us.</p>
</blockquote>

<h2>Overview</h2>

<p>Molecular docking is a key step in virtual drug screening. AutoDock Vina, as an open-source molecular docking software, offers advantages such as high speed and accurate algorithms, making it particularly suitable for building virtual screening based on molecular docking. It is used based on the MGLTools toolkit. MGLTools includes AutoDock Tools (ADT) and Python Molecular Viewer (PMV). ADT is used to generate input files for Vina, and PMV is used to view results. For more information, please refer to AutoDock Vina and MGLTools documentation.</p>

<h2>Prerequisites</h2>

<p>To deploy the AutoDock Vina Community Edition service instance, you need to access and create certain Alibaba Cloud resources. Therefore, your account must have permissions for the following resources.</p>
<p><strong>Note:</strong> Permissions need to be added only when your account is a RAM user.</p>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Permission Policy Name</th>
            <th>Remarks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AliyunECSFullAccess</td>
            <td>Permission to manage Elastic Compute Service (ECS)</td>
        </tr>
        <tr>
            <td>AliyunVPCFullAccess</td>
            <td>Permission to manage Virtual Private Cloud (VPC)</td>
        </tr>
        <tr>
            <td>AliyunROSFullAccess</td>
            <td>Permission to manage Resource Orchestration Service (ROS)</td>
        </tr>
        <tr>
            <td>AliyunEHPCFullAccess</td>
            <td>Permission to manage Elastic High Performance Computing (EHPC)</td>
        </tr>
        <tr>
            <td>AliyunNASFullAccess</td>
            <td>Permission to manage File Storage (NAS)</td>
        </tr>
        <tr>
            <td>AliyunComputeNestUserFullAccess</td>
            <td>User-side permission to manage Compute Nest services</td>
        </tr>
    </tbody>
</table>

<h2>Billing Description</h2>

<p>The costs for deploying AutoDock Vina Community Edition on Compute Nest mainly involve:</p>
<ul>
    <li>Elastic High Performance Computing (EHPC) cluster fees</li>
    <li>File System (NAS) fees</li>
    <li>Traffic bandwidth fees</li>
</ul>

<h2>Deployment Architecture</h2>

<ul>
    <li>The deployment consists of one EHPC cluster, which includes manager nodes, scheduler nodes, and compute nodes.</li>
    <li>The service uses NAS-CPFS to build a high-performance shared file system.</li>
</ul>

<h2>Parameter Description</h2>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Parameter Group</th>
            <th>Parameter Item</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3">Service Instance</td>
            <td>Service Instance Name</td>
            <td>Length must not exceed 64 characters. Must start with an English letter. Can contain numbers, English letters, hyphens (-), and underscores (_).</td>
        </tr>
        <tr>
            <td>Region</td>
            <td>The region where the service instance is deployed.</td>
        </tr>
        <tr>
            <td>Billing Method</td>
            <td>Billing type for resources: Pay-As-You-Go and Subscription.</td>
        </tr>
        <tr>
            <td rowspan="6">EHPC Cluster Configuration</td>
            <td>Cluster Login Password</td>
            <td>Length: 8-30 characters. Must contain at least three of the following: uppercase letters, lowercase letters, digits, and special symbols ()`~!@#$%^&*-+=|{}[]:;'<>,.?/</td>
        </tr>
        <tr>
            <td>EHPC Deployment Mode</td>
            <td>Tiny, Simple, Standard</td>
        </tr>
        <tr>
            <td>Compute Node Instance Type</td>
            <td>Specifications for compute nodes available in the availability zone.</td>
        </tr>
        <tr>
            <td>Number of Compute Nodes</td>
            <td>Number of compute nodes. Valid values: 1-99.</td>
        </tr>
        <tr>
            <td>Login Node Instance Type</td>
            <td>Specifications for login nodes available in the availability zone.</td>
        </tr>
        <tr>
            <td>Number of Management Nodes</td>
            <td>Number of management nodes. Valid values: 1, 2, 4.</td>
        </tr>
        <tr>
            <td rowspan="2">EHPC Cluster User Configuration</td>
            <td>User Password</td>
            <td>Length: 8-30 characters. Must contain at least three of the following: uppercase letters, lowercase letters, digits, and special symbols ()~!@#$%^&*-_+=\|{}[]:;'/<>,.?/</td>
        </tr>
        <tr>
            <td>Username</td>
            <td>The username used to log in to the cluster. Default is "lammps".</td>
        </tr>
        <tr>
            <td rowspan="3">Network Configuration</td>
            <td>Availability Zone</td>
            <td>The availability zone where the ECS instances are located.</td>
        </tr>
        <tr>
            <td>VPC ID</td>
            <td>The VPC where the resources are located.</td>
        </tr>
        <tr>
            <td>VSwitch ID</td>
            <td>The VSwitch where the resources are located.</td>
        </tr>
    </tbody>
</table>

<h2>Deployment Process</h2>

<ol>
    <li>
        <p>Visit the Compute Nest AutoDock Vina Community Edition <a href="https://computenest.console.aliyun.com/user/cn-hangzhou/serviceInstanceCreate?ServiceId=service-7ef89f7679cb4813b4a3" target="_blank">deployment link</a> and fill in the deployment parameters as prompted.</p>
    </li>
    <li>
        <p>After filling in the parameters, you can view the corresponding price inquiry details. Confirm the parameters and click <strong>Next: Confirm Order</strong>.</p>
    </li>
    <li>
        <p>After confirming the order, agree to the service agreement and click <strong>Create Now</strong> to enter the deployment phase.</p>
    </li>
</ol>

<h2>Usage Process</h2>

<h3>Step 1: Connect to the Cluster via Console</h3>

<ol>
    <li>Log in to the <a href="https://ehpc.console.aliyun.com" target="_blank">Elastic High Performance Computing Console</a>.</li>
    <li>In the top menu bar, select the region in the upper left corner.</li>
    <li>In the left-side navigation pane, click <strong>Clusters</strong>.</li>
    <li>On the <strong>Clusters</strong> page, find the target cluster deployed via Compute Nest and click <strong>Remote Connection</strong>.</li>
    <li>On the <strong>Remote Connection</strong> page, enter the cluster username, login password, and port, then click <strong>SSH Connection</strong>.</li>
</ol>

<h3>Step 2: Submit Jobs</h3>

<p>This article simulates the interaction process between small molecule ligands and biological macromolecule receptors to predict the binding mode and affinity between the ligand and receptor, thereby simulating drug screening. Currently widely used commercial compound libraries such as Specs, Enamine, and ChemDiv can provide a large number of ligands to simulate interactions with given receptors. Since there are no dependencies between different ligands, they can be processed in large-scale parallelism. This article is also applicable to other biological and medical scenarios with requirements for large batches and high concurrency processing.</p>

<ol>
    <li>
        <p><strong>Download and extract job files.</strong></p>
        <p><em>Note: If git is not installed in the cluster, please execute <code>sudo yum install -y git</code> to install git first.</em></p>
        <p>Download job files:</p>
        <pre><code>git clone https://code.aliyun.com/best-practice/022.git</code></pre>
        <p>Extract job files:</p>
        <pre><code>cd 022
tar xzvf vina-ehpcarrayjob.tar.gz</code></pre>
    </li>
    <li>
        <p><strong>Modify the configuration file.</strong></p>
        <pre><code>cd vina-ehpcarrayjob
vim conf.txt</code></pre>
        <p>In <code>conf.txt</code>, delete the following two lines:</p>
        <pre><code>receptor = 1fkn_rgd.pdbqt
ligand = $file</code></pre>
    </li>
    <li>
        <p><strong>Create the job script, named vina.sh.</strong></p>
        <pre><code>cd /home/vinatest
vim vina.sh</code></pre>
        <p>The script content is as follows:</p>
        <pre><code>#!/bin/bash

#PBS -N vina_job
#PBS -l nodes=1:ppn=2
#PBS -l walltime=00:10:00
#PBS -j oe
#PBS -v receptor="022/vina-ehpcarrayjob/1fkn_rgd.pdbqt",ligand="022/vina-ehpcarrayjob/test/ligand_1.pdbqt",config="022/vina-ehpcarrayjob/conf.txt"


cd $PBS_O_WORKDIR

ppn="$NCPUS"
cd $PBS_O_WORKDIR


vina --receptor $receptor --config $config  --ligand $ligand --out out.pdbqt --cpu $ppn</code></pre>
    </li>
    <li>
        <p><strong>Submit the job.</strong></p>
        <pre><code>qsub vina.sh</code></pre>
        <p>The expected return is as follows, indicating that the generated job ID is 0.scheduler.</p>
        <pre><code>0.scheduler</code></pre>
    </li>
</ol>

<h3>Step 3: View Job Results</h3>

<ol>
    <li>
        <p><strong>Check job status.</strong></p>
        <pre><code>qstat -x 0.scheduler</code></pre>
        <p>The expected return is as follows. When 'S' in the return information is 'R', it means the job is running; when 'S' is 'F', it means the job has finished.</p>
        <pre><code>Job id            Name             User              Time Use S Queue
----------------  ---------------- ----------------  -------- - -----
0.scheduler       vina_job         vinatest          00:01:56 F workq </code></pre>
    </li>
    <li>
        <p><strong>Use VNC visualization to view job results.</strong></p>
        <ol>
            <li>
                <p>Open VNC. The system will automatically open port 12016 in the cluster security group during console operations.</p>
                <ol>
                    <li>In the left-side navigation pane of the <a href="https://ehpc.console.aliyun.com" target="_blank">Elastic High Performance Computing Console</a>, click <strong>Clusters</strong>.</li>
                    <li>On the <strong>Clusters</strong> page, find the target cluster, click <strong>More</strong> &gt; <strong>VNC</strong>.</li>
                    <li>Use VNC to remotely connect to the visualization service. For specific operations, please refer to <a href="https://help.aliyun.com/zh/e-hpc/user-guide/use-vnc-to-manage-a-visualization-service#section-bf6-eyn-edu" target="_blank">Connect to Visualization Service</a>.</li>
                </ol>
            </li>
            <li>In the VNC window, select <strong>Application &gt; System Tools &gt; Terminal</strong>.</li>
            <li>Execute the command in the Terminal: <code>/usr/local/bin/adt /home/vinatest/022/vina-ehpcarrayjob/1fkn_rgd.pdbqt /home/vinatest/out.pdbqt</code> to open AutoDock Tools and load the job results.</li>
            <li>After loading the model in the pop-up AutoDock Tools window, the results are displayed as follows:</li>
        </ol>
    </li>
</ol>
