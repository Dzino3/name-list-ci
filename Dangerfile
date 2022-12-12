#!/usr/bin/env ruby

# Validate PR description
pr_body_text = github.pr_body.strip.gsub(/\s+/, ' ')
body_threshold = 10
is_short_description = (pr_body_text.length < github.pr_title.length) && (pr_body_text.length <= body_threshold)

if is_short_description
  warn "`404` Pull Request description not found :disappointed: \nWrite a convincing description of your PR and why we should land it"
end

# Validate commit message
contribution_file = '.github/CONTRIBUTING.md'
issue_regex = '(.*(#|gh-)[1-9][0-9]*.*)'
merge_or_revert_regex = '(Merge .+|Revert .+)'
commit_regex = "(#{issue_regex}|#{merge_or_revert_regex})"

git.commits.each do |commit|
  commit_message = commit.message.lines.first.chomp.strip.gsub(/\s+/, ' ')
  warn "Commit message `#{commit_message}` does not follow the [Contribtuion Rules](#{contribution_file})!" if commit_message !~ /#{commit_regex}/
end
