# PRしたファイルの直近のコミット履歴を表で可視化する

require "logger"
require "git"
g = Git.open("./", :log => Logger.new(STDOUT))

files = (git.added_files + git.modified_files) #=> FileList

markdown "## あなたが修正したファイルに関する直近のコミット\n\n"
data = []
reviewer = nil
files.each do |f|

	# gitからそのファイルの履歴を取得する
	# XXX PRのコミットでない
	#logs = git.commits
	logs = g.gblob(f).log(10)

	message = "### #{f}\n\n"
	message << "date | commit | msg | user |\n"
	message << "| --- | ----- | --- | --- |\n"

	tmp = []
	logs.each do |log|
		d = {
			:user => log.author.name,
			:id => log,
			:date => log.date,
			:msg => log.message,
		}
		tmp.push(d)
	    message << "| #{d[:date]} | #{d[:id]} | #{d[:msg]} | #{d[:user]} |\n"	

		# TODO 自分以外
		reviewer = d[:user]
	end

	data.push(tmp)
	message << "\n\n"
	markdown message

	# TODO 直近のコミッタをレビューアに設定する
	
end

github.pr_json["reviewers"] = reviewer
message "#{reviewer}さんをレビューアにします"

