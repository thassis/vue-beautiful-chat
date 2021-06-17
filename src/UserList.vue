<template>
  <div class="user-list" :style="{background: userListColor.userList.bg}">
    <table style="padding-top: 5px">
      <tbody>
        <tr v-for="user in participants" :key="user.id">
          <td style="text-align: center">
            <img :src="user.imageUrl" class="img-msg" />
          </td>

          <td class="user-element" :style="{color: userListColor.userList.text}">
            <div class="user-row">
              <div style="width: 80%">
                <table>
                  <tr>
                    <td>
                      <a
                        style="color: #4f4f4f; font-weight: bold; font-size: 16px; cursor: pointer"
                        @click="toggleUserList(user.id)"
                      >
                        {{ user.name }}
                      </a>
                    </td>
                  </tr>
                  <tr>
                    <td style="display: flex">
                      <a
                        style="text-align: end; color: #aaaa; font-size: 14px; cursor: pointer"
                        @click="toggleUserList(user.id)"
                      >
                        {{ user.lastMessage }}
                      </a>
                    </td>
                  </tr>
                </table>
              </div>
              <a
                v-if="user.unreadMsgUser"
                style="
                  display: flex;
                  font-weight: bold;
                  justify-content: center;
                  align-items: center;
                  color: white;
                  font-size: 10px;
                  width: 20px;
                  height: 20px;
                  cursor: pointer;
                  background-color: #ff4646;
                  border-radius: 15px;
                "
                @click="toggleUserList(user.id)"
              >
                {{ user.unreadMsgUser }}
              </a>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    participants: {
      type: Array,
      required: true
    },
    colors: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
      inUserList: true
    }
  },
  computed: {
    userListColor() {
      const defaultColors = {
        userList: {
          bg: '#FFFFFF',
          text: '#000000'
        }
      }
      return Object.assign(defaultColors, this.colors)
    }
  },
  methods: {
    toggleUserList(user_id) {
      console.log('clicouuyy', user_id)
      this.inUserList = !this.inUserList
      this.$emit('userList', this.inUserList, user_id)
    }
  }
}
</script>

<style scoped>
.user-list {
  height: 100%;
  overflow: auto;
  padding-left: 5px;
  padding-top: 8px;
}
.img-msg {
  border-radius: 50%;
  width: 45px;
  height: 45px;
  object-fit: fill;
  margin-right: 5px;
}
.user-element {
  width: 90%;
  font-size: 20px;
  vertical-align: middle;
}
.user-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  width: 90%;
  border-bottom-style: solid;
  border-color: #aaaa;
  border-bottom-width: 1px;
}
</style>
