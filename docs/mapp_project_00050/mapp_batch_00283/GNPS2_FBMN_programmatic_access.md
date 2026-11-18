# GNPS2 programmatic upload and FBMN submission

**Finding:** Programmatic **file upload is documented** for eligible collaborators through SFTP; **self-service programmatic launch of a hosted FBMN job is not documented**. The official FBMN instructions instead direct anyone seeking programmatic access to contact Mingxun Wang at `mingxun.wang@ucr.edu`. Do not treat the GNPS2 workflow-input URL or the workflow's Nextflow source as a documented job-submission API. [Upload documentation](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fileupload/) · [FBMN documentation](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fbmn/) · [GNPS2 API page](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/api/) · [FBMN workflow source](https://github.com/Wang-Bioinformatics-Lab/Feature_Based_Molecular_Networking_Workflow/blob/master/Makefile)

## Upload

- The normal browser route requires login, then **File Browser → create a folder → upload/drag files**; uploads cannot go directly into the user's root folder. [Official upload guide](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fileupload/)
- For **collaborators whose SFTP accounts are activated**, GNPS2 documents `sftp.gnps2.org` on port `443`, authenticated with GNPS2 username/password. The guide labels bulk SFTP/FTP access **beta** and says not all accounts are enabled. Its verified example for uploading a folder is: [Official upload guide](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fileupload/#sftp-file-uploads)

  ```sh
  sftp -P 443 <username>@sftp.gnps2.org:/ <<< $'put -r <folder name>'
  ```

- For very large uploads, GNPS2 recommends depositing a public MassIVE dataset and selecting the data using USIs instead. [Official upload guide](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fileupload/#bulk-uploads)

## Launch

- The documented hosted route is to sign in at [the FBMN input form](https://gnps2.org/workflowinput?workflowname=feature_based_molecular_networking_workflow), or choose **Launch Workflows → feature_based_molecular_networking_workflow → Launch Workflow**; select the feature table (CSV/TXT) and MS/MS summary (MGF/MSP), optionally metadata, then set the processing tool/parameters. [Official FBMN guide](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fbmn/#launch-fbmn-workflows-on-gnps2) · [Input requirements](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fbmn/#requirement-for-the-fbmn-workflow)
- First-party [`workflowinput.yaml`](https://github.com/Wang-Bioinformatics-Lab/Feature_Based_Molecular_Networking_Workflow/blob/master/workflowinput.yaml) confirms the workflow name and form fields `inputfeatures`, `inputspectra`, optional `metadata_filename`, and `featurefindingtool`. These are **workflow input configuration**, not evidence of a public HTTP submission endpoint. [Workflow configuration](https://github.com/Wang-Bioinformatics-Lab/Feature_Based_Molecular_Networking_Workflow/blob/master/workflowinput.yaml)
- The official [GNPS2 API page](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/api/) has `TODO` under “GNPS2” and lists other services (e.g. structure search, public dataset files), but **no authenticated upload or hosted FBMN job-launch API contract**. This establishes a documentation gap, not that automation is impossible. The explicit next step for hosted programmatic FBMN is [contacting Mingxun Wang](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fbmn/#introduction) for access/interface details; do not invent a POST endpoint, authentication flow, or payload.
- The first-party [`Makefile`](https://github.com/Wang-Bioinformatics-Lab/Feature_Based_Molecular_Networking_Workflow/blob/master/Makefile) runs `nextflow run ./nf_workflow.nf` locally for development/testing; it does **not** submit a GNPS2-hosted job. [Workflow README](https://github.com/Wang-Bioinformatics-Lab/Feature_Based_Molecular_Networking_Workflow/blob/master/README.md)

**Access conditions:** The hosted form requires GNPS2 login, SFTP needs account activation, and the current GNPS2 login page states the free service is for academic/non-profit use; industry/commercial users require a license. [FBMN guide](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fbmn/) · [Upload guide](https://wang-bioinformatics-lab.github.io/GNPS2_Documentation/fileupload/) · [GNPS2 login terms](https://gnps2.org/login)
