# Arm DevSummit 2021: Introducing Keil Studio

Successful IoT implementations require collaboration and a robust ecosystem of support and tools. Keil Studio cloud embraces the Open-CMSIS-Pack initiative and provides a cloud-native platform with direct Git integration for collaboration of distributed teams, and modern CI workflows for rapid development.

This introductory workshop allows attendees to experience the workflow first-hand. They will prototype an IoT end node application, connect it to the cloud, and debug it via their browser.

## Pre-work

- Keil Studio Cloud runs in a browser. You need a Chromium based browser (Chrome/Edge - no matter if you run Windows, Mac, or Linux).
- Create a user account at [studio.keil.arm.com](studio.keil.arm.com) and ensure you can login. If you have an Arm or Mbed account, you can use these to access the site.
- The workshop uses the [NXP IMXRT1050-EVKB](https://www.keil.arm.com/hardware/IMXRT1050-EVKB/) to download and debug to the target:
  - Please make sure that the latest FW for the debug adapter is installed. Follow the instructions on the [Guide](https://www.keil.arm.com/hardware/IMXRT1050-EVKB/guide/) tab (“CMSIS-DAP Firmware” section).
  - If you do not have access to the board, you can still follow much of the workshop. Debug will be demonstrated by the facilitators of the workshop.
- We recommend a dual monitor setup, so that you can see the workshop and your Keil Studio workspace at the same time.

## Optional pre-work

Two of the projects shown in the workshop require additional accounts being set up:

- Set up a [GitHub](https://www.github.com) account for forking one of the example projects.
- Set up an AWS account if you want to follow the last step in the tutorial:
  - Create an account at [aws.amazon.com](aws.amazon.com).
  - For the workshop, you need to configure a Thing in the AWS IoT console. You also need to have copies of your client certificate and private key available. For creation, follow [these instructions](https://github.com/MDK-Packs/Documentation/tree/master/AWS_Thing).

## Required hardware

For the best workshop experience, you'll need the following:

- [NXP IMXRT1050-EVKB](https://www.keil.arm.com/hardware/IMXRT1050-EVKB/) (if you don’t have the hardware, you can still follow most of the workshop).
- Ethernet cable long enough to connect the board to your router.
- 5V USB power supply with Micro-USB cable to supply the dev board.
- Optional: SparkFun WiFi Shield DA16200.

## Slides

The following slide deck contains screenshots of the workshop. Use it to recreate the workshop in your own pace.

## Further reading

Here's a list of additional resources that you may find useful:

- A DevSummit session that explains the background of the workshop: [CI/CD and MLOps workflow for IoT endpoint development](https://devsummit.arm.com/en/sessions/145)
- A blog, similar to the above: [Cloud-based embedded development to supercharge IoT](https://www.arm.com/blogs/blueprint/cloud-based-embedded-development)
- Blog about [Cloud infrastructure for continuous integration tests](https://community.arm.com/developer/tools-software/tools/b/tools-software-ides-blog/posts/infrastructure-for-continuous-integration-tests)

## Feedback

If you want to get in touch, please raise an issue or send in a PR.
