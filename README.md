# R-based analysis of INCLUDE data on Cavatica

## Creating a Cavatica Project
1. Go to *Projects* tab > Create a project.
2. Enter a project name.
3. Under General information:  
   Set Billing group (e.g. Pilot Funds, DS3_2024). 
   Set Spot Instances if desired. 
4. Under Advanced settings:  
   Allow network access (IMPORTANT).  
5. Click Create.
6. You should then be taken to the Dashboard for your new project.  
   You may want to edit the project description.  


## Pushing data from the INCLUDE Data Hub to Cavatica

### INCLUDE Data Hub
1. Connect your INCLUDE and Cavatica accounts  
Within the Data Hub, ensure you are (still) connected to Cavatica:   
Dashboard > Cavatica Projects > Connect. 
>[!IMPORTANT]
>You will need to have two-factor authentication enabled for your Cavatica account or you will get an error 
2. For this example, filter to HTP MSD data files (n = 477).  
   Data Exploration > Participant > Study Code = HTP.  
   Data Exploration > Biospecimen > Sample Type = Plasma.  
   Data Exploration > Data File > Experimental Strategy = Multiplex Immunoassay.  
   May want to save Filter...  
3. Select all files that you want to analyze.  
4. Click on *Analyse in Cavatica* button.  
   Select the Cavatica Project to which you want to copy files.  
   Click on Copy files.  

### Cavatica
Within Cavatica, ensure you are (still) connected to the INCLUDE Data Hub:  
Account Settings > Dataset Access > INCLUDE DRS Server > Connect / Reconnect.  

5. Go to the project to which you copied the files.  
   The copied files should now be available in the *Files* tab.  

## Using Cavatica/Data Studio
1. Start an *Analysis* instance.  

   a. New *Analysis*:  
      - Go to *Data Studio* tab > Create new analysis.  
      - Set analysis name.  
      - Select RStudio (JupyterLab also available).  
      - Select latest R version in Environment setup (eg R 4.3.2 - BioC 3.18).  
      - Select Instance type, Attached Storage, Suspend Time (may affect cost).  
      - Click on Start and wait for instance to initialize.  

   b. Existing *Analysis*:  

      - Go to *Data Studio* tab.  
      - Click on Start and wait for instance to initialize.  

2. You should now be in an RStudio instance.  

   a. To create a new Project by cloning from Github. 
    
      - Go to File > New Project... > Version Control > Git.  
      - Enter Repository URL.  
      - May want to modify Project directory name.  
      - Click on Create Project.  
      - May need to enter Github Username and PAT.  
      - Once project opens in RStudio, in R console run `renv::init()` to initialize project and install required packages (renv should already be available).  

   b. Previously created *Analyses* should resume with R Project already open in RStudio.  

      - If not, go to File > Open Project... > Select .Rproj file.  
      - Once project opens in RStudio, in R console run `renv::restore()` to restore project and re-install required packages.  

3. Open analysis R script(s) and work as usual. 

4. Copy R Project to `/sbgenomics/output-files/` for later access/download (see notes below).  

## Tips for working with RStudio sessions in Data Studio
* Once Data Studio instances are terminated, after idle timeout or manually, the R environment does not persist (including any newly installed R packages).
  However, running `renv::restore()` will reinstall packages from local project cache based on `renv.lock` file.  

* Data Studio working dir is:  
  `/sbgenomics/workspace`  
  R Project working directory will usually be:  
  `/sbgenomics/workspace/<R_PROJECT_NAME>`  
  Files in these directories can be previewed, but not accessed, by clicking on the *Analysis Name* in the *Data Studio* tab.

* Cavatica Project *Files* (eg files transferred from INCLUDE Data Hub) can be accessed here:  
  `/sbgenomics/project-files`  
  This directory is read-only from within Data Studio

* To be accessible outside Data Studio, via the *Files* tab in your Cavatica Project, files will need to be copied to: 
  `/sbgenomics/output-files/`  
  Any files or dirs copied to this location **will not be accessible until after the Data Studio instance is terminated**.  
  Saving of these files upon termination ~~may~~ will take several minutes.
