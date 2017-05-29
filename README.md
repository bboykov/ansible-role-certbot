# Ansible Role: Certbot (for Let's Encrypt)

## Requirements

Certbot requires Git to be installed.

## Role Variables

    certbot_repo: https://github.com/certbot/certbot.git
    certbot_version: master
    certbot_keep_updated: yes

Certbot code repository options. This role clones the agent from the configured repo, then makes the `certbot-auto` script executable.

    certbot_dir: /opt/certbot

The directory inside which Certbot will be cloned.

    certbot_auto_renew: true
    certbot_auto_renew_user: "{{ ansible_user }}"
    certbot_auto_renew_hour: 3
    certbot_auto_renew_minute: 30

By default, this role configures a cron job to run under the provided user account at the given hour and minute, every day. The defaults run `certbot-auto renew` via cron every day at 03:30:00 by the user you use in your Ansible playbook. It's preferred that you set a custom user/hour/minute so the renewal is during a low-traffic period and done by a non-root user account.

## Dependencies

None.

## Example Playbook

    - hosts: servers

      vars:
        certbot_auto_renew_user: your_username_here
        certbot_auto_renew_minute: 20
        certbot_auto_renew_hour: 5

      roles:
        - certbot
