FROM danielflook/terraform-github-actions-base:latest

COPY entrypoints/ /entrypoints/
COPY actions.sh /usr/local/actions.sh

COPY tools/convert_validate_report.py /usr/local/bin/convert_validate_report
COPY tools/github_pr_comment.py /usr/local/bin/github_pr_comment
COPY tools/latest_terraform_version.py /usr/local/bin/latest_terraform_version
COPY tools/convert_output.py /usr/local/bin/convert_output
COPY tools/plan_cmp.py /usr/local/bin/plan_cmp
COPY tools/convert_version.py /usr/local/bin/convert_version
COPY tools/workspace_exists.py /usr/local/bin/workspace_exists
COPY tools/compact_plan.py /usr/local/bin/compact_plan
COPY tools/format_tf_credentials.py /usr/local/bin/format_tf_credentials

RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config \
 && echo "IdentityFile /.ssh/id_rsa" >> /etc/ssh/ssh_config \
 && mkdir -p /.ssh

RUN curl -L https://github.com/cloudposse/tfmask/releases/download/0.7.0/tfmask_linux_amd64 -o /usr/bin/tfmask
RUN chmod +x /usr/bin/tfmask

COPY tools/http_credential_actions_helper.py /usr/bin/git-credential-actions
RUN git config --system credential.helper /usr/bin/git-credential-actions \
 && git config --system credential.useHttpPath true \
 && ln -s /usr/bin/git-credential-actions /usr/bin/netrc-credential-actions

LABEL org.opencontainers.image.title="GitHub actions for terraform"
