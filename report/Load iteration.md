# Enterprise Linux Lab Report

- Student name: Jorn Creten
- Github repo: <https://github.com/HoGentTIN/elnx-2021-ha-JornCreten>

The goals of the first iteration are to set up the lamp stack and a simple load balancing tool (haproxy).

## Requirements

- nginx splash page
- postgresql database install
- simple load balancing

## Test plan

How are you going to verify that the requirements are met? The test plan is a detailed checklist of actions to take, including the expected result for each action, in order to prove your system meets the requirements. Part of this is running the automated tests, but it is not always possible to validate *all* requirements throught these tests.

## Documentation

- Started out by figuring out how ansible works, how roles & playbooks work together and how to set them up
- Followed by setting up a simple LAMP-stack with nginx & postgresql
- Set up the firewall for this server
- Set up haproxy with the config files, system processes etc
- Set up firewall for the load balancer
- Checked if it worked, next step would be converting all this work into an ansible playbook
- Ansible documentation & stackoverflow were the main help with this 

## Test report

The test report is a transcript of the execution of the test plan, with the actual results. Significant problems you encountered should also be mentioned here, as well as any solutions you found. The test report should clearly prove that you have met the requirements.

## Resources

List all sources of useful information that you encountered while completing this assignment: books, manuals, HOWTO's, blog posts, etc.
