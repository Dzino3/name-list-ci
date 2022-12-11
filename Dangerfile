#!/usr/bin/env ruby

# Validate PR description
pr_body_text = github.pr_body.strip.gsub(/\s+/, ' ')
trivial_threshold = 10
is_short_description = (pr_body_text.length < github.pr_title.length) && (pr_body_text.length <= trivial_threshold)
is_trivial_code_change = git.lines_of_code <= trivial_threshold

if is_short_description && !is_trivial_code_change
  warn "`404` Pull Request description not found :disappointed: \nWrite a convincing description of your PR and why we should land it"
end

# Validate commit message
contribution_file = '.github/CONTRIBUTING.md'
commit_regex = '(.*(#|gh-)[1-9][0-9]*.*)'
git.commits.each do |commit|
  commit_message = commit.message.lines.first.chomp.strip.gsub(/\s+/, ' ')
  warn "Commit message `#{commit_message}` does not follow the [Contribtuion Rules](#{contribution_file})!" if commit_message !~ /#{commit_regex}/
end
