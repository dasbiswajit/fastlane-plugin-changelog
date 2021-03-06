# Ensure there is a summary for a PR
fail "Please provide a summary in the Pull Request description" if github.pr_body.length < 5

# Only accept PRs to the `develop` branch
fail "Please re-submit this PR to develop, we may have already fixed your issue." if github.branch_for_base != "master"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Request a CHANGELOG entry, and give an example
has_app_changes = !git.modified_files.grep(/lib/).empty?
if !git.modified_files.include?('CHANGELOG.md') && has_app_changes
  fail("Please include a CHANGELOG entry to credit yourself! \nYou can find it at [CHANGELOG.md](https://github.com/pajapro/fastlane-plugin-changelog/blob/#{github.branch_for_head}/CHANGELOG.md).", :sticky => false)
  markdown <<-MARKDOWN
Here's an example of your CHANGELOG entry under [`[Unreleased]`](https://github.com/pajapro/fastlane-plugin-changelog/blob/#{github.branch_for_head}/CHANGELOG.md#unreleased) section:
```markdown
### Fixed:
- #{github.pr_title}
```
MARKDOWN
end