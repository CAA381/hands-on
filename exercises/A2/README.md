# Lesson A – Setting up CI/CD pipeline
# Exercise A2 - Creating your first pipeline

## Enter Deployment Credentials
Open Google Chrome and navigate to localhost:8080 to open the user interface.

1. Click on **Credentials**.

![](../../images/a/a2_credentials.png)

2. Click on **Jenkins**.

![](../../images/a/a2_jenkins.png)

3. Click on **Global Credentials**.

![](../../images/a/a2_global_credentials.png)

4. Click on **Add Credentials**.

![](../../images/a/a2_add_credentials.png)


5. In the ID box fill in **CF-DEPLOY**.

![](../../images/a/a2_id_cf_deploy.png)


6. In the Description box fill in again **CF-DEPLOY**.

![](../../images/a/a2_desc_cf_deploy.png)

7. For user enter **CAA381-\<your partisipantId@teched.cloud.sap>** in the box.

![](../../images/a/a2_enter_user.png)

8. For password enter the password provided to you via the paper sheets.

![](../../images/a/a2_enter_pass.png)

9. Save your changes by clicking **OK**.

![](../../images/a/a2_click_ok.png)

10. Go Back to the Jenkins home page.

![](../../images/a/a2_back_to_jenkins.png)

## Setup Pipeline

Once we have setup our credential it is time to proceed to our pipeline. 

1. On Jenkins home page click on **Create new jobs**.

![](../../images/a/a2_create_new-job.png)

2. Name the job as **teched2019**.

![](../../images/a/a2_name_job.png)

3. Click on **Multibranch Pipeline**.

![](../../images/a/a2_multibranch_pipeline.png)


4. Click on **OK**.

![](../../images/a/a2_ok.png)

5. In the Branch Sources click on the **Add Source** dropdown button and select **Git**.

![](../../images/a/a2_source_git.png)

6. As project repository enter **http://cloudl000024.wdf.sap.corp:8080/teched/caa381**.

![](../../images/a/a2_project_repo.png)

7. Now in the **Behaviors** section click on the **Add** dropdown buttona and select **Filter by name(with regular expression)**.

![](../../images/a/a2_filter_by_name.png)

8. Your configuration should look like this.

![](../../images/a/a2_summary_screen.png)

9. Enter in the **Regular Expression** field **your participant id**.

![](../../images/a/a2_porject_id.png)

10. Click on **Save**.

![](../../images/a/a2_click_save.png)

11. In the navigation to the left click **Open Blue Ocean**.

![](../../images/a/a2_open_blue_ocean.png)

12. In the navigation to the left click **Open Blue Ocean**.

![](../../images/a/a2_open_blue_ocean.png)


13. In the blue ocean click on **your participant id**

![](../../images/a/a2_participant-id.png)


14. You now should see your pipeline

![](../../images/a/a2_pipeline.png)




[![](../../images/nav-previous.png) Previous Exercise](../A1/README.md) ｜[![](../../images/nav-home.png) Overview page](../../README.md) ｜ [![](../../images/nav-next.png) Next Exercise](../exercises/prep/B.md)
