<template>
  <div class="w-full">
    <!-- component -->
    <div class="container mx-auto px-4 sm:px-8">
      <div class="py-8">
        <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
          <div
            class="inline-block min-w-full shadow rounded-lg overflow-hidden"
          >
            <div class="flex flex-row justify-between p-4 bg-gray-700">
              <input
                type="text"
                class="w-1/5 rounded p-2 text-gray-400"
                placeholder="Search by name"
                v-model="searchQuery"
              />
              <div class="flex flex-row justify-end">
                <button
                  :disabled="currentPage <= 1"
                  :class="[
                    currentPage <= 1
                      ? 'text-gray-400 hover:underline '
                      : 'text-white',
                  ]"
                  @click="setPage(currentPage - 1)"
                  class="pr-2 border-1"
                >
                  prev
                </button>
                <button
                  :disabled="currentPage === totalPages"
                  :class="[
                    currentPage === totalPages
                      ? 'text-gray-400 hover:underline '
                      : 'text-white',
                  ]"
                  @click="setPage(currentPage + 1)"
                  class="pr-2 border-1 hover:underline text-white"
                >
                  next
                </button>
              </div>
            </div>
            <p
              class="w-full bg-gray-100 text-gray-800 text-center p-4"
              v-if="$fetchState.pending"
            >
              Loadin...
            </p>
            <p
              class="w-full bg-gray-100 text-gray-400 text-center p-4"
              v-else-if="$fetchState.error"
            >
              Server Error, Please, try again later.
              <span class="text-blue-400 p-4"
                ><button @click="$fetch">Refresh</button>
              </span>
            </p>
            <table v-else class="min-w-full leading-normal bg-gray-400">
              <thead>
                <tr>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                    "
                  >
                    #
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                    "
                  >
                    Name
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                    "
                  >
                    Form
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                    "
                  >
                    Total.Pts
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      lg:table-cell
                    "
                  >
                    GS
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      lg:table-cell
                    "
                  >
                    A
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      lg:table-cell
                    "
                  >
                    CS
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      lg:table-cell
                    "
                  >
                    GC
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      lg:table-cell
                    "
                  >
                    OG
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      lg:table-cell
                    "
                  >
                    PS
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      md:table-cell
                    "
                  >
                    PM
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                    "
                  >
                    YC
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      xl:table-cell
                    "
                  >
                    RC
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      xl:table-cell
                    "
                  >
                    S
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      xl:table-cell
                    "
                  >
                    B
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      xl:table-cell
                    "
                  >
                    BPS
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      xl:table-cell
                    "
                  >
                    TSB
                  </th>
                  <th
                    class="
                      px-5
                      py-3
                      border-b-2 border-gray-200
                      bg-gray-100
                      text-center text-xs
                      font-semibold
                      text-gray-600
                      uppercase
                      tracking-wider
                      hidden
                      xl:table-cell
                    "
                  >
                    £
                  </th>
                </tr>
              </thead>

              <tbody class="bg-gray-100">
                <tr
                  v-for="player of paginatedList"
                  :key="player.id"
                  class="text-gray-600 bg-gray-100"
                >
                  <td class="px-5 py-5 border-b border-gray-200 text-sm">
                    <p class="text-gray-900 whitespace-no-wrap">
                      {{ getType(player.element_type) }}
                    </p>
                  </td>
                  <td class="px-5 py-5 border-b border-gray-200 text-sm">
                    <div class="flex items-center">
                      <p class="text-gray-900 whitespace-no-wrap">
                        {{ player.first_name }}
                        <span class="font-bold">{{ player.web_name }}</span>
                      </p>
                    </div>
                  </td>
                  <td class="px-5 py-5 border-b border-gray-200 text-sm">
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.form }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      lg:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      api
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      lg:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.goals_scored }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      lg:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.assists }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      lg:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.clean_sheets }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      lg:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.goals_conceded }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      lg:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.own_goals }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      md:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.penalties_saved }}
                    </p>
                  </td>
                  <td class="px-5 py-5 border-b border-gray-200 text-sm">
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.penalties_missed }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.yellow_cards }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.red_cards }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.saves }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.bonus }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.bps }}
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      {{ player.selected_by_percent }}%
                    </p>
                  </td>
                  <td
                    class="
                      px-5
                      py-5
                      border-b border-gray-200
                      text-sm
                      hidden
                      xl:table-cell
                    "
                  >
                    <p class="text-gray-900 whitespace-no-wrap text-center">
                      £{{ (player.now_cost / 10).toFixed(1) }}
                    </p>
                  </td>
                </tr>
              </tbody>
            </table>
            <p class="w-full p-2 text-gray-400 bg-gray-100 text-right">
              <span v-if="currentPage != totalPages"
                >{{
                  currentPage * paginatedList.length -
                  (paginatedList.length - 1)
                }}
                to {{ currentPage * paginatedList.length }}</span
              ><span v-else>
                {{ currentPage * playersPerPage - (playersPerPage - 1) }}
                to
                {{
                  currentPage * playersPerPage -
                  (playersPerPage - paginatedList.length)
                }}
              </span>
              of
              <span>{{ players.length }}</span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      players: [],
      player_types: [],
      playersPerPage: 10,
      currentPage: 1,
      totalPlayers: 0,
      searchQuery: '',
      apiError: false,
    }
  },
  computed: {
    totalPages() {
      if (this.totalPlayers == 0) {
        return 1
      } else {
        return Math.ceil(this.totalPlayers / this.playersPerPage)
      }
    },
    paginatedList() {
      if (this.searchQuery == '') {
        var filteredLists = this.players
      } else {
        var filteredLists = this.players.filter((player) => {
          for (var key in player) {
            if (
              String(player[key])
                .toLowerCase()
                .indexOf(this.searchQuery.toLowerCase()) !== -1
            ) {
              return true
            }
          }
          return false
        })
      }
      this.totalPlayers = filteredLists.length
      if (this.currentPage >= this.totalPages) {
        this.currentPage = this.totalPages
      }
      var index = this.currentPage * this.playersPerPage - this.playersPerPage
      return filteredLists.slice(index, index + this.playersPerPage)
    },
  },
  methods: {
    setPage(pageNumber) {
      this.currentPage = pageNumber
    },
    getType(id) {
      var playerType = null
      this.player_types.forEach((type) => {
        if (type.id == id) {
          console.log('found id : ' + type.id)
          console.log('type: ' + type.singular_name_short)
          playerType = type.singular_name_short
        }
      })
      return playerType
    },
  },
  async fetch() {
    this.players = await fetch('https://fantasy.premierleague.com/api/bootstrap-static/').then(
      (res) => {
        console.log(res.json())
        return res.json()
      }
    )
    this.player_types = await fetch(
      'http://localhost:8000/api/players/types'
    ).then((res) => res.json())
    this.totalPlayers = this.players.length
  },
}
</script>
