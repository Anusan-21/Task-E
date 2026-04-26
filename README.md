# Task E: Compliance and Supply Chain

## Mapping to SSDF Practice PS.1 (Protect Software)

### The Evidence


![yml](screenshots/yml.png)

The build process is defined in the `.github/workflows/generate-sbom.yml` file, specifically using the above configuration

![github-action-success](screenshots/github-action-success.png)

### The Argument

The use of GitHub Actions establishes a controlled environment for generating software artifacts, which prevents the security risks associated with building code on local hardware. Local machines are often unverified and may contain malware or allow for manual, undocumented changes to the source code before a build is completed. By delegating the build to a hosted Ubuntu runner, the process is restricted to a standardized environment that is created specifically for each task and triggered only by verified commits to the repository

### The Conclusion

This automated workflow reduces the possibility of human tampering during the build phase. By ensuring that every version of the software is produced through a transparent and isolated pipeline, the project directly adheres to the security requirements of NIST SSDF PS.1

## Mapping to SSDF Practice PW.4 (Produce Well-Secured Software)

### The Evidence

![flask_version](screenshots/flask_version.png)

The above snippet from the `sbom.json` file demonstrates the detailed tracking of third-party components within the software release

### The Argument

The generated SBOM serves as a definitive ingredient list, offering full visibility into the nested third-party libraries contained within the Docker environment. Unlike traditional development where internal dependencies are often undocumented, this record allows for immediate identification of components. If a vulnerability is reported in a specific package, the exact version and license data can be verified in seconds, rather than requiring an manual audit of the entire codebase


### The Conclusion

By automatically capturing detailed metadata for every library during the build phase, the project maintains the comprehensive provenance records required by NIST SSDF PW.4


## Mapping to SSDF Practice RV.1 (Respond to Vulnerabilities)

### The Evidence

![json-evidence](screenshots/json-evidence.png)

The above configuration within the `generate-sbom.yml` file ensures the SBOM is generated in a machine-readable format

### The Argument

The pipeline is configured to output the SBOM in JSON format rather than a static document like a PDF. While a PDF is easy for a person to read, it cannot be easily processed by security tools at scale. By using the CycloneDX JSON standard, the software's components can be automatically and continuously cross-referenced against global vulnerability databases(CVEs). This allows for the immediate detection of new security threats as soon as they are published, without requiring manual intervention from the development team

### The Conclusion

The use of a standardized, machine-readable format ensures that vulnerability discovery is an automated, continuous process. This allows for the ongoing monitoring of the software supply chain, directly fulfilling the requirements of NIST SSDF RV.1





